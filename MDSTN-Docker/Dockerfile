# Use a base image with Python and build tools
FROM ubuntu:22.04

# Set environment variables to non-interactive  
ENV DEBIAN_FRONTEND=noninteractive

# Install system dependencies
RUN apt update && apt install -y \
    build-essential \
    python3 \
    python3-venv \
    python3-pip \
    r-base \
    git \
    wget \
    curl \
    libcurl4-openssl-dev \
    libssl-dev \
    && apt clean

# Create app directory
WORKDIR /app

# Clone the MDSTN repo
RUN git clone https://github.com/ELO-Lab/MDSTN.git .
RUN mkdir -p cec2013/p1-stn  # Avoid R errors if folders don't exist yet

# Create and activate Python virtual environment
RUN python3 -m venv /app/.venv
ENV PATH="/app/.venv/bin:$PATH"

# Install Python packages
RUN pip install --upgrade pip && \
    pip install numpy pandas tqdm

# Install R packages
RUN Rscript -e 'install.packages(c("igraph", "ggplot2", "RColorBrewer", "gifski"), repos="https://cloud.r-project.org")'

# Build the C++ code
RUN make

# Set default command to bash so you can run scripts interactively
CMD ["/bin/bash"]
