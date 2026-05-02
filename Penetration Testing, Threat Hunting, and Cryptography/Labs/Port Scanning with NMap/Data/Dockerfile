FROM kalilinux/kali-rolling
 
# Add Kali archive signing key directly (no apt needed)
ADD https://archive.kali.org/archive-keyring.gpg \
    /usr/share/keyrings/kali-archive-keyring.gpg
 
RUN chmod 644 /usr/share/keyrings/kali-archive-keyring.gpg
 
# Configure Kali repository with signed-by
RUN echo "deb [signed-by=/usr/share/keyrings/kali-archive-keyring.gpg] \
http://http.kali.org/kali kali-rolling main contrib non-free non-free-firmware" \
> /etc/apt/sources.list
 
# Now apt works correctly
RUN apt-get clean && apt-get update
 
# Install required packages
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y \
    ccrypt \
    nano \
    tzdata \
    libbsd0 \
    ca-certificates \
    wget \
    gnupg \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*
 
WORKDIR /
 
CMD ["bash"]