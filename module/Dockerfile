FROM registry.gitlab.com/snapcoreinc/snapcore-monitor:latest as kickstart

# yuo can start from scratch if your exe use no shared lirbaries
FROM alpine:3.12

COPY --from=kickstart /tini .
COPY --from=kickstart /dih-monitor /dih-monitor

# your module lives in folder ./module
# from here you can compile, fetch, aggregate the image

# Populate example here - i.e. "cat", "sha512sum" or "node index.js"
ENV startup_process="echo 'hello world'"
ENV mode="stdio" 
ENV http_proxy=""
ENV https_proxy=""

# Port to the monitor
EXPOSE 8080

# Only when it's a cmd line app
HEALTHCHECK --interval=3s CMD [ -e /tmp/.lock ] || exit 1

ENTRYPOINT ["/tini", "--"]
CMD ["/dih-monitor"]
