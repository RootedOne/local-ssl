# Guide to Obtaining a Subdomain SSL with Win-ACME (PEM Format)[cite: 1]

If you want to get a free SSL certificate (Let's Encrypt) for your subdomain and receive the files in `.pem` format, this guide is for you[cite: 1].

## Prerequisites[cite: 1]
*   You must have downloaded the `wacs.exe` application[cite: 1].
*   You must have access to your domain's DNS management panel (e.g., Cloudflare, your hosting panel, etc.)[cite: 1].

## The Single-Line Command[cite: 1]
Simply open your terminal (PowerShell or CMD) as an **Administrator** and copy/paste this command, replacing the placeholders with your own details[cite: 1]:
```powershell
wacs.exe --source manual --host sub.yourdomain.com --validation manual --validationmode dns-01 --store pemfiles --pemfilespath "C:\Certificates" --installation none
```
[cite: 1]

### What does this command do?[cite: 1]
*   `--host`: Enter your subdomain address here[cite: 1].
*   `--validation manual`: Indicates that you will set the DNS record yourself[cite: 1].
*   `--store pemfiles`: Provides the files in `.pem` format (instead of the Windows Certificate Store)[cite: 1].
*   `--pemfilespath`: The folder path where you want the files saved[cite: 1].

---

## Step-by-Step Instructions[cite: 1]

1.  **Run the Command:** Execute the code above[cite: 1]. The program will start and eventually provide you with a **Host** and a **Value**[cite: 1]. For example, it will tell you to create a TXT record with the name `_acme-challenge.sub` and a specific long value[cite: 1].

2.  **Set the DNS Record:**[cite: 1]
    *   Go to your domain's DNS management panel[cite: 1].
    *   Create a new record of type **TXT**[cite: 1].
    *   In the Name or Host field, enter the name provided by the program (e.g., `_acme-challenge.sub`)[cite: 1].
    *   In the Value or Text field, paste the long code provided by the program[cite: 1].
    *   Set the TTL to the lowest possible value (e.g., 60 seconds)[cite: 1].

3.  **Wait and Confirm:**[cite: 1]
    *   Wait a minute for the record to propagate across the internet[cite: 1].
    *   Return to the terminal and press **Enter**[cite: 1].

4.  **Success:** If everything is correct, the certificate files will appear in your specified directory (e.g., `C:\Certificates`)[cite: 1].

## What files are provided?[cite: 1]
In the output folder, you will see these files:[cite: 1]
*   `*-crt.pem`: The certificate itself[cite: 1].
*   `*-key.pem`: The private key (very important and confidential!)[cite: 1].
*   `*-chain.pem`: The certificate chain[cite: 1].
*   `*-chain-as-bundle.pem`: A combination of the certificate and the chain (commonly used for Nginx and Apache)[cite: 1].

---
**Important Note:** Because this is a "manual" method, it does not support auto-renewal[cite: 1]. You will need to run this command again every 90 days and set a new DNS record[cite: 1].
