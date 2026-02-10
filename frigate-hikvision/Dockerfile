# ARG defines the version we want to hijack (default to latest stable or specific tag)
ARG FRIGATE_VERSION=stable

# Pull the official image
FROM ghcr.io/blakeblackshear/frigate:${FRIGATE_VERSION}

# Standard practice: Set working directory
WORKDIR /opt/frigate

# --- SURGERY START ---

# 1. Remove the original files that don't work with Hikvision
RUN rm frigate/ptz/onvif.py
RUN rm frigate/ptz/autotrack.py

# 2. Copy our "Patched" files from your repo into the image
COPY patches/onvif.py frigate/ptz/onvif.py
COPY patches/autotrack.py frigate/ptz/autotrack.py

# 3. (Optional) Print a message during build to confirm surgery was successful
RUN echo "Hikvision Patch Applied: Swapped onvif.py and autotrack.py"

# --- SURGERY END ---

# standard entrypoint (inherited from base, but good to be explicit if needed)
# No need to change CMD or ENTRYPOINT usually, as we just swapped python files.
