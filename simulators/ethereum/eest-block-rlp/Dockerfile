# This simulation feeds clients the Ethereum Execution Spec Tests as block rlp upon startup.
FROM python:3.10-slim

# Install git and wget
RUN apt-get update && \
    apt-get install -y git wget && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

RUN git clone --depth 1 --branch verkle/pydantic-rebase https://github.com/spencer-tb/execution-spec-tests.git

WORKDIR execution-spec-tests

RUN wget https://github.com/spencer-tb/execution-spec-tests/releases/download/verkle-transition-v0/fixtures.tar.gz

RUN tar xfz fixtures.tar.gz
RUN find fixtures/ -name '._*' -exec rm '{}' \;
RUN rm -rf fixtures/assets/ fixtures/report_fill.html
RUN ls -a fixtures/
RUN ls -a fixtures/blockchain_tests

# ENV PIP_NO_WARN_SCRIPT_LOCATION=1  # this doesn't remove the warning
RUN pip install --upgrade pip
RUN pip install -e .

# Consume Spencer's released fixtures
ENTRYPOINT ["pytest", "-c", "src/pytest_plugins/consume/ini_files/pytest-consume-rlp.ini", "--input", "fixtures/blockchain_tests/", "-v"]

# This should be simpler... but bugs
# ENTRYPOINT ["consume", "rlp", "--input=https://github.com/spencer-tb/execution-spec-tests/releases/download/verkle-transition-v0/fixtures.tar.gz", "-v"]