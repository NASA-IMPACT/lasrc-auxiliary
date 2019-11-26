ARG AWS_ACCOUNT_ID=000000000000
FROM ${AWS_ACCOUNT_ID}.dkr.ecr.us-west-2.amazonaws.com/hls-base
ENV PREFIX=/usr/local \
		L8_AUX_DIR=/usr/local/src

ENTRYPOINT ["/bin/sh", "-c"]
CMD ["updatelads.py","--today"]
