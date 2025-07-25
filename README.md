# How to Upgrade Your Drosera Node

A simple guide to upgrade your Drosera operator node without breaking anything. Follow the steps below 👇

---

## 1. Stop your Docker or systemD

### If using Docker:
```bash
cd ~
cd ~/Drosera-Network
docker compose down -v
```

### If using systemD:
```bash
sudo systemctl stop drosera
sudo systemctl disable drosera
```

---

## 2. Update Drosera:
```bash
cd ~
curl -LO https://github.com/drosera-network/releases/releases/download/v1.19.0/drosera-operator-v1.19.0-x86_64-unknown-linux-gnu.tar.gz
tar -xvf drosera-operator-v1.19.0-x86_64-unknown-linux-gnu.tar.gz

sudo cp drosera-operator /usr/bin
drosera-operator --version
```

---

## 3. Install Docker Image
```bash
docker pull ghcr.io/drosera-network/drosera-operator:latest
```

---

## 4. Apply New RPC:

1. Navigate to your Drosera configuration directory:
    ```bash
    cd ~
    cd my-drosera-trap
    nano drosera.toml
    ```

2. Update the `drosera_rpc` in the file:
    Replace:
    ```toml
    drosera_rpc = "http://seed-node.testnet.drosera.io"
    ```
    With:
    ```toml
    drosera_rpc = "https://relay.testnet.drosera.io"
    ```

3. Save the file and run the following command:
    ```bash
    DROSERA_PRIVATE_KEY=your_private_key drosera apply
    ```

---

## 5. Open port:
```bash
sudo ufw allow ssh
sudo ufw allow 22/tcp
sudo ufw allow 22/udp
sudo ufw allow 31313/tcp
sudo ufw allow 31313/udp
sudo ufw allow 31314/tcp
sudo ufw allow 31314/udp
sudo ufw enable
sudo ufw reload
```

## 6. Run the Node:

### If using Docker:
```bash
cd ~
cd Drosera-Network
docker compose up -d
```

### If using systemD:
```bash
sudo systemctl daemon-reload
sudo systemctl enable drosera
sudo systemctl start drosera
```

---

After completing the steps, your node should now be running successfully, and you will see a green status ✅.

---

## Additional Resources:

- **Join Drosera Community**: [Drosera Discord](https://discord.gg/drosera)
- **Node Guide**: [Drosera Network GitHub](https://github.com/HeavenOG/Drosera-Network)
