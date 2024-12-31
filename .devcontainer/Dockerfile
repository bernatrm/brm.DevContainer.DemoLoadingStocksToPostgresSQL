ARG BASE_VARIANT=datascience-notebook
ARG IMAGE_VARIANT=latest

FROM quay.io/jupyter/${BASE_VARIANT}:${IMAGE_VARIANT}

# Crea el directorio de la aplicación
WORKDIR /workspace

# Copia el requirements.txt
COPY src/requirements.txt /workspace/src/requirements.txt

USER root
# Generally, Dev Container Features assume that the non-root user (in this case jovyan)
# is in a group with the same name (in this case jovyan). So we must first make that so.
RUN groupadd jovyan \
    && usermod -g jovyan -a -G users jovyan

USER jovyan

# Instala las dependencias
RUN pip install --upgrade pip && pip install -r /workspace/src/requirements.txt

CMD ["jupyter", "lab", "--ip=0.0.0.0", "--port=8888", "--no-browser", "--NotebookApp.token=''"]
