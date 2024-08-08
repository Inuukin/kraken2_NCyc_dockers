FROM python:3.9-slim

ENV DEBIAN_FRONTEND=noninteractive
ENV KNEADDATA_VERSION=0.12.0
ENV TRIMMOMATIC_VERSION=0.39
ENV TRIMMOMATIC_DIR=/opt/trimmomatic
ENV FASTQC_VERSION=0.11.9
ENV FASTQC_DIR=/opt/fastqc

RUN apt-get update && \
    apt-get install -y \
    build-essential \
    zlib1g-dev \
    libbz2-dev \
    liblzma-dev \
    libcurl4-openssl-dev \
    libssl-dev \
    libncurses5-dev \
    libncursesw5-dev \
    wget \
    unzip \
    default-jre \
    bowtie2 \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

RUN pip install kneaddata==${KNEADDATA_VERSION}

RUN mkdir -p ${TRIMMOMATIC_DIR} && \
    wget -O ${TRIMMOMATIC_DIR}/trimmomatic-${TRIMMOMATIC_VERSION}.zip \
    http://www.usadellab.org/cms/uploads/supplementary/Trimmomatic/Trimmomatic-${TRIMMOMATIC_VERSION}.zip && \
    unzip ${TRIMMOMATIC_DIR}/trimmomatic-${TRIMMOMATIC_VERSION}.zip -d ${TRIMMOMATIC_DIR} && \
    rm ${TRIMMOMATIC_DIR}/trimmomatic-${TRIMMOMATIC_VERSION}.zip

ENV PATH="${TRIMMOMATIC_DIR}/Trimmomatic-${TRIMMOMATIC_VERSION}:${PATH}"

RUN ln -s ${TRIMMOMATIC_DIR}/Trimmomatic-${TRIMMOMATIC_VERSION}/trimmomatic-${TRIMMOMATIC_VERSION}.jar /usr/local/bin/trimmomatic.jar

RUN mkdir -p ${FASTQC_DIR} && \
    wget -O ${FASTQC_DIR}/fastqc_v${FASTQC_VERSION}.zip \
    https://www.bioinformatics.babraham.ac.uk/projects/fastqc/fastqc_v${FASTQC_VERSION}.zip && \
    unzip ${FASTQC_DIR}/fastqc_v${FASTQC_VERSION}.zip -d ${FASTQC_DIR} && \
    chmod +x ${FASTQC_DIR}/FastQC/fastqc && \
    ln -s ${FASTQC_DIR}/FastQC/fastqc /usr/local/bin/fastqc && \
    rm ${FASTQC_DIR}/fastqc_v${FASTQC_VERSION}.zip

