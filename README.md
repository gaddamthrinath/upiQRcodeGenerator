# Generate UPI QR Code

This Node.js script generates a UPI QR Code for a specified payment. The QR code can be used for making payments through UPI-compatible apps.

## Prerequisites

- Node.js installed on your system
- `qrcode` package installed

Install the required package using npm:
```bash
npm install qrcode
```

## How It Works

1. **Define UPI Payment Details**: Provide details like UPI ID, recipient name, amount, and a transaction note.
2. **Generate UPI String**: Construct a UPI payment string in the format `upi://pay?...`.
3. **Generate QR Code**: Use the `qrcode` package to generate a QR code based on the UPI string.
4. **Save QR Code**: Save the QR code as a PNG file in the project directory.

## Script

```javascript
const QRCode = require('qrcode');

// Function to generate UPI QR code
const generateUPIQRCode = async () => {
  // Define UPI payment details
  const upiData = {
    payeeVPA: 'example@upi', // UPI ID of the recipient
    payeeName: 'John Doe',   // Name of the recipient
    amount: 100.50,          // Amount in INR this Amount can be diynamic like getting from i.e const {amount} req.body
    transactionNote: 'Payment for services' // Optional note
  };

  // Construct UPI string
  const upiString = `upi://pay?pa=${upiData.payeeVPA}&pn=${upiData.payeeName}&am=${upiData.amount}&cu=INR&tn=${upiData.transactionNote}`;

  try {
    // Generate QR code
    const qrCode = await QRCode.toDataURL(upiString);
    console.log('UPI QR Code generated successfully.');
    console.log(qrCode); // This will be a base64 image string

    // Optionally, save it to a file
    const fs = require('fs');
    const base64Data = qrCode.replace(/^data:image\/png;base64,/, '');
    fs.writeFileSync('upi_qr_code.png', base64Data, 'base64');
    console.log('QR Code saved as upi_qr_code.png');
  } catch (error) {
    console.error('Error generating QR code:', error);
  }
};

generateUPIQRCode();
```

## Usage

1. Clone or download the script to your local machine.
2. Install the required packages by running:
   ```bash
   npm install qrcode
   ```
3. Run the script:
   ```bash
   node script_name.js
   ```
4. After execution, the QR code will be generated and saved as `upi_qr_code.png` in the project directory.

## Example

### Input
```javascript
const upiData = {
  payeeVPA: 'example@upi',
  payeeName: 'John Doe',
  amount: 100.50,
  transactionNote: 'Payment for services'
};
```

### Output
- **Console Output**:
  ```
  UPI QR Code generated successfully.
  QR Code saved as upi_qr_code.png
  ```
- **File**: A PNG file named `upi_qr_code.png` containing the QR code.

## License

This project is licensed under the MIT License. Feel free to use and modify it as needed.
