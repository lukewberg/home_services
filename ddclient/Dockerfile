FROM debian:latest
ARG CLOUDFLARE_API_KEY

RUN apt-get update && apt-get install -y ddclient && apt-get install -y ca-certificates

RUN update-ca-certificates --fresh

RUN apt-get clean

# Edit the /etc/ddclient.conf file to include your dynamic DNS provider's settings
RUN cat <<EOL > /etc/ddclient.conf
daemon=300
usev4=webv4
webv4=checkip.dyndns.com/
protocol=cloudflare
zone=lukewberg.dev
login=token
password=$CLOUDFLARE_API_KEY
vpn.lukewberg.dev
EOL

# Generic entrypoint for testing to keep the container running
# ENTRYPOINT ["tail", "-f", "/dev/null"]

ENTRYPOINT ["ddclient", "--foreground", "--verbose", "--noquiet"]