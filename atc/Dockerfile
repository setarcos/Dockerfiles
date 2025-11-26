FROM python:3.11-slim

ENV DEBIAN_FRONTEND=noninteractive
ENV TZ=Asia/Shanghai
ENV CANN_TOOLKIT="Ascend-cann-toolkit_8.3.RC2_linux-x86_64.run"

WORKDIR /home/ascend

RUN sed -i 's/deb.debian.org/mirrors.pku.edu.cn/g' /etc/apt/sources.list.d/debian.sources

RUN pip3 install -i https://mirrors.tuna.tsinghua.edu.cn/pypi/web/simple attrs \
    cython \
    'numpy>=1.19.2,<=1.24.0' \
    decorator \
    sympy \
    cffi \
    pyyaml \
    pathlib2 \
    psutil \
    protobuf==3.20.0 \
    scipy \
    requests \
    absl-py

RUN groupadd -g 1000 ascend && useradd -u 1000 -g ascend -s /bin/bash ascend

COPY ${CANN_TOOLKIT} /tmp/

RUN chmod +x /tmp/${CANN_TOOLKIT} && \
    /tmp/${CANN_TOOLKIT} --install --quiet && \
    rm -f /tmp/${CANN_TOOLKIT}

ENV ASCEND_HOME=/usr/local/Ascend
ENV PATH=$ASCEND_HOME/ascend-toolkit/latest/bin:$PATH
ENV LD_LIBRARY_PATH=$ASCEND_HOME/ascend-toolkit/latest/x86_64-linux/devlib:$ASCEND_HOME/ascend-toolkit/latest/lib64:$ASCEND_HOME/nnae/latest/lib64:$LD_LIBRARY_PATH
ENV PYTHONPATH=$ASCEND_HOME/ascend-toolkit/latest/python/site-packages:$ASCEND_HOME/ascend-toolkit/latest/opp/op_impl/built-in/ai_core/tbe:$PYTHONPATH

RUN echo "source $ASCEND_HOME/ascend-toolkit/set_env.sh" >> /home/ascend/.bashrc && \
    apt-get update && \
    apt-get upgrade -y && \
    apt-get install -y --no-install-recommends build-essential && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* && \
    chown ascend:ascend -R /home/ascend

USER ascend

WORKDIR /home/ascend

CMD ["/bin/bash"]
