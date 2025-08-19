# create_jwt.py README

This script is designed to generate a JWT token signed with X.509 certificates for use in Siemens MindSphere device integrations or similar scenarios.

## Usage

Run the script using the following command:

```
python create_jwt.py <device_name> <tenant_name>
```

**Parameters:**
- `<device_name>`: Specify your device name. (A `.pem` and `.key` file with the same name must exist)
- `<tenant_name>`: Specify your tenant name. (A `.pem` file with the same name must exist)

## Required Files

The following files must be present in the directory for the script to work properly:
- `<device_name>.pem`: X.509 certificate for the device (in PEM format)
- `<tenant_name>.pem`: X.509 certificate for the tenant (in PEM format)
- `<device_name>.key`: Private key file for the device (in PEM format)

## What the Script Does

1. Reads the device and tenant name from command line arguments.
2. Reads the related certificate files and adds their base64-encoded content in the JWT `x5c` header.
3. Prepares the JWT payload (fields such as jti, iss, sub, aud, iat, exp, schemas, ten).
4. Signs the JWT using the private key with RS256 algorithm.
5. Outputs the signed JWT token.

## Dependencies

You need to have the following Python packages installed:
- `PyJWT`
- `cryptography`

To install, run:
```bash
pip install pyjwt cryptography
```

## Example Run

```
python create_jwt.py myDevice myTenant
```

If successful, the output will be your signed JWT token.

## Notes

- The script strips the BEGIN/END lines (`-----BEGIN CERTIFICATE-----` / `-----END CERTIFICATE-----`) from your certificates and only uses the base64 data.
- Token validity is 1 hour (`exp` claim).
- Your private key file must be unencrypted or you need to adapt the code to handle encrypted keys.

---
