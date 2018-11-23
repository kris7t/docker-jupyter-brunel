FROM kris7t/rise-notebook

USER root

RUN apt-get -y update && \
    apt-get install --no-install-recommends -y openjdk-8-jre-headless ca-certificates-java && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

USER $NB_UID

# Must install jupyter-pip and brunel in two separate commands,
# otherwise brunel install fails because it cannot load jupyterpip.
RUN pip install --no-cache-dir jupyter-pip && \
    pip install --no-cache-dir brunel && \
    cp -r /home/$NB_USER/.local/share/jupyter/nbextensions/brunel_ext /opt/conda/share/jupyter/nbextensions/ && \
    ln -s /opt/conda/share/jupyter/nbextensions/brunel_ext/sumoselect/sumoselect.css /opt/conda/share/jupyter/nbextensions/brunel_ext/sumoselect.css && \
    ln -s /opt/conda/share/jupyter/nbextensions/brunel_ext/sumoselect/jquery.sumoselect.min.js /opt/conda/share/jupyter/nbextensions/brunel_ext/jquery.sumoselect.min.js && \
    rm -rf /home/$NB_USER/.local && \
    fix-permissions $CONDA_DIR && \
    fix-permissions /home/$NB_USER
