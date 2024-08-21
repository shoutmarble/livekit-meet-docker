# livekit-meet-docker with Sozu reverse proxy

This repository is dedicated to deploying a video conferencing application using LiveKit with Docker. It serves as a demonstration and is meant for testing and development purposes, not for production use. The `meet` component is a sample application to showcase how LiveKit can be integrated and utilized.

## Project Structure

This project is composed of the following main components:

- `meet`: A sample video conferencing application powered by LiveKit. This is not intended for real-world production use.
- `livekit`: The LiveKit server.
- ~`caddy`: A Caddy server functioning as a reverse proxy.~
- `sozu`: A Sozu server functioning as a reverse proxy.

## Setup

Follow these steps to get the project up and running:

1. **Clone the repository:**

    ```bash
    git clone https://github.com/shoutmarble/livekit-meet-docker
    cd livekit-meet-docker
    ```

2. **Copy the `.env.example` file to create a `.env` file and set the necessary environment variables:**

    ```bash
    cp .env.example .env
    ```

3. **Generate an API key and secret using the `generate_keypair.py` script:**

    ```bash
    python3 generate_keypair.py
    ```

4. **Edit** the `.env` and `livekit.yaml` files with the generated keys and appropriate domain names. This is required to run the application correctly.

5. **Edit the `livekit.yaml` lines #127/`keys:` #246/`domain:`

    ```YAML
    keys:
    7e510eafd39852bee31c4d5bfa87847e: 083ca120732019b2cf4a350d1c928173
    ```
    
    ```YAML
    external_tls: true
    # needs to match tls cert domain
    domain: turn.landingdev.xyz
    ```
6. create a directory called `certificates` and place your certificates there needed for `compose.yml`
    ```
    -rwxrwxrwx 1 root root 3591 Aug 15 11:38 example.com.crt*
    -rwxrwxrwx 1 root root 1802 Aug 15 11:38 example.com.issuer.crt*
    -rwxrwxrwx 1 root root  235 Aug 15 11:38 example.com.json*
    -rwxrwxrwx 1 root root 1679 Aug 15 11:38 example.com.key*
    -rwxrwxrwx 1 root root 5270 Aug 15 11:38 example.com.pem*
    ```
6. **Build and launch the project using Docker:**

    ```bash
    docker-compose up --build
    ```

## Required Domains and Ports

You will need three publicly accessible servers, configured with the following domains:
- LIVEKIT_MEET_FQDN=livekit-meet.example.com
- LIVEKIT_SERVER_FQDN=livekit-server.example.com
- LIVEKIT_TURN_FQDN=livekit-turn.example.com

Please ensure the following ports are open:
- 80 - TLS issuance
- 443 - primary HTTPS and TURN/TLS
- 3478/UDP - TURN/UDP
- 7881 - WebRTC over TCP
- 7882/UDP - WebRTC over UDP

## Additional Resources

- For more on the `meet` application component, visit the repository: [LiveKit Meet](https://github.com/livekit-examples/meet)

## License

This project is released under the MIT License. For more details, please refer to the [LICENSE](./LICENSE) file.
