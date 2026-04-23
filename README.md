# Guide to Obtaining a Subdomain SSL with Win-ACME (PEM Format)

If you want to get a free SSL certificate (Let's Encrypt) for your subdomain and receive the files in `.pem` format, this guide is for you.

## Prerequisites
*   You must have downloaded the `wacs.exe` application.
*   You must have access to your domain's DNS management panel (e.g., Cloudflare, your hosting panel, etc.).

## The Single-Line Command
Simply open your terminal (PowerShell or CMD) as an **Administrator** and copy/paste this command, replacing the placeholders with your own details:
```powershell
wacs.exe --source manual --host sub.yourdomain.com --validation manual --validationmode dns-01 --store pemfiles --pemfilespath "C:\Certificates" --installation none
```


### What does this command do?
*   `--host`: Enter your subdomain address here.
*   `--validation manual`: Indicates that you will set the DNS record yourself.
*   `--store pemfiles`: Provides the files in `.pem` format (instead of the Windows Certificate Store).
*   `--pemfilespath`: The folder path where you want the files saved.

---

## Step-by-Step Instructions

1.  **Run the Command:** Execute the code above. The program will start and eventually provide you with a **Host** and a **Value**. For example, it will tell you to create a TXT record with the name `_acme-challenge.sub` and a specific long value.

2.  **Set the DNS Record:**
    *   Go to your domain's DNS management panel.
    *   Create a new record of type **TXT**.
    *   In the Name or Host field, enter the name provided by the program (e.g., `_acme-challenge.sub`).
    *   In the Value or Text field, paste the long code provided by the program.
    *   Set the TTL to the lowest possible value (e.g., 60 seconds).

3.  **Wait and Confirm:**
    *   Wait a minute for the record to propagate across the internet.
    *   Return to the terminal and press **Enter**.

4.  **Success:** If everything is correct, the certificate files will appear in your specified directory (e.g., `C:\Certificates`).

## What files are provided?
In the output folder, you will see these files:
*   `*-crt.pem`: The certificate itself.
*   `*-key.pem`: The private key (very important and confidential!).
*   `*-chain.pem`: The certificate chain.
*   `*-chain-as-bundle.pem`: A combination of the certificate and the chain (commonly used for Nginx and Apache).

---
**Important Note:** Because this is a "manual" method, it does not support auto-renewal. You will need to run this command again every 90 days and set a new DNS record.
