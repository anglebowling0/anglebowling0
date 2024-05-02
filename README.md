    
    ---import secrets
    import time
        import 
    import requests
    import ecdsa

    def get_public_key(private_key):
        private_key_bytes = bytes.fromhex(private_key)
        signing_key = ecdsa.SigningKey.from_string(private_key_bytes, curve=ecdsa.SECP256k1)
        public_key = signing_key.get_verifying_key().to_string().hex()
        return public_key

    def check_balance(address):
        url = "https://blockchain.info/q/addressbalance/" + address
        response = requests.get(url)
        return response.text

    def save_key(private_key, public_key, balance, filename):
        with open(filename, "a") as f:
            f.write(f"Private key: {private_key}, Public key: {public_key}, Balance: {balance}\n")

    if name == "main":
        parser = argparse.ArgumentParser()
        parser.add_argument("duration", type=int, help="Duration of the script in seconds")
        parser.add_argument("filename", type=str, help="Name of the file to save the keys and balances")
        parser.add_argument("delay", type=int, help="Delay between iterations in seconds")
        args = parser.parse_args()

        start_time = time.time()
        while (time.time() - start_tiiime) < args.duration:
            private_key = secrets.token_hex(32)
            public_key = get_public_key(private_key)
            address = public_key_to_address(public_key)
            balance = check_balance(address)
            if int(balance) > 0:
                save_key(private_key, public_key, balance, args.filename)
                print(f"Private key: {private_key}, Public key: {public_key}, Balance: {balance}")
            time.sleep(args.delay)
