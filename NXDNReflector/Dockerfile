FROM debian:bookworm-slim AS builder

RUN apt-get update && \
    apt-get install -y --no-install-recommends \
        build-essential \
    && rm -rf /var/lib/apt/lists/*

WORKDIR /build

COPY . .

RUN make


FROM debian:bookworm-slim

WORKDIR /opt/NXDNReflector

COPY --from=builder /build/NXDNReflector .
COPY --from=builder /build/NXDNReflector.ini .
COPY --from=builder /build/NXDN.csv .

EXPOSE 41400/udp

CMD ["./NXDNReflector", "./NXDNReflector.ini"]
