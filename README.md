# Instrucciones para lanzar tutorial de Caffe con JupyterHub en Guane #

1. Crear una carpeta llamada **jupyter**

2. Guardar el siguiente script bajo el nombre **jupyter.batch**

3. Ejecutar el script usando **sbatch jupyter.batch**

        #!/bin/sh
        #SBATCH --partition=all
        #SBATCH --time=00:15:00
        #SBATCH --nodes=1
        #SBATCH --job-name="Caffe"
        #SBATCH --output=jupyterhub.out
        #SBATCH --exclusive
        #SBATCH --ntasks-per-node=1
        #SBATCH --gres=gpu:4

        cp /opt/jupyterhub/jupyterhub_config.py .
        export PATH=/usr/local/caffeDigits/python:$PATH
        sudo jupyterhub

Consultamos el nodo reservado con **squeue** y accedemos de la siguiente manera:

Guane13 = www.sc3.uis.edu.co/guaneJ13

---


