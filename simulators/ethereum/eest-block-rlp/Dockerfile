# This simulation feeds clients the Ethereum Execution Spec Tests as block rlp upon startup.
FROM python:3.10-slim

# Install git and wget
RUN apt-get update && \
    apt-get install -y git wget && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# Install execution-spec-tests
RUN git clone -b feat/pytest/add-a-verify-fixtures-as-a-separate-pytest-command https://github.com/danceratopz/execution-spec-tests.git
WORKDIR /execution-spec-tests
RUN pip install -e .

ENTRYPOINT ["consume", "rlp", "--input", "https://github.com/ethereum/execution-spec-tests/releases/download/v1.0.6/fixtures_develop.tar.gz"]
