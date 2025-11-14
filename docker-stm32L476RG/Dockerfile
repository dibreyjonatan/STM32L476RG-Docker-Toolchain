FROM ubuntu:latest

#je vais installer tout ce dont j'aurais besoin pour compiler le code pour le STM32L476RG

RUN apt-get update && apt-get install -y --no-install-recommends \
    build-essential \
    gcc-arm-none-eabi \
    gdb-multiarch \
    libusb-1.0-0-dev \
    libtool \
 && rm -rf /var/lib/apt/lists/*
        
# Je crée le dossier CMSIS
RUN mkdir /cmsis    
# Maintenant je copie les fichiers CMSIS et STM32CubeL4 nécessaires
COPY CMSIS /cmsis  

