FROM tensorflow/tensorflow:2.1.2-gpu-jupyter

#RUN apt-get update && apt-get upgrade -y \
RUN apt-get update \
    && apt-get install -y \
        build-essential \
        git \
        sudo \
        cmake \
        unzip zip
#    && rm -rf /var/lib/apt/lists/*

RUN pip install scikit-learn

RUN pip install pandas psutil

ARG username
ARG userid

ARG home=/home/${username}
ARG workdir=${home}/handson-ml2

RUN adduser ${username} --uid ${userid} --gecos '' --disabled-password \
    && echo "${username} ALL=(root) NOPASSWD:ALL" > /etc/sudoers.d/${username} \
    && chmod 0440 /etc/sudoers.d/${username}

WORKDIR ${workdir}
RUN chown ${username}:${username} ${workdir}

USER ${username}
WORKDIR ${workdir}


#...


# INFO: Uncomment the RUN command below for easy and constant notebook URL (just localhost:8888)
#       That will switch Jupyter to using empty password instead of a token.
#       To avoid making a security hole you SHOULD in fact not only uncomment but
#       regenerate the hash for your own non-empty password and replace the hash below.
#       You can compute a password hash in any notebook, just run the code:
#          from IPython.lib import passwd
#          passwd()
#       and take the hash from the output
#RUN mkdir -p ${home}/.jupyter && \
#    echo 'c.NotebookApp.password = u"sha1:c6bbcba2d04b:f969e403db876dcfbe26f47affe41909bd53392e"' \
#    >> ${home}/.jupyter/jupyter_notebook_config.py
RUN mkdir -p ${home}/.jupyter && \
    echo 'c.NotebookApp.token = u"handson-ml2-docker"' \
    >> ${home}/.jupyter/jupyter_notebook_config.py
