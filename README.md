# Instrucciones para lanzar tutorial de Caffe con JupyterHub en Guane #

1. Crear una carpeta llamada **jupyter**

2. Guardar el siguiente script bajo el nombre **jupyter.batch**

3. Ejecutar el script usando **sbatch jupyter.batch**

        #!/bin/sh
        #SBATCH --partition=all
        #SBATCH --time=02:00:00
        #SBATCH --nodes=1
        #SBATCH --job-name="Caffe"
        #SBATCH --output=jupyterhub.out
        #SBATCH --exclusive
        #SBATCH --ntasks-per-node=1
        #SBATCH --gres=gpu:1

        cp /opt/jupyterhub/jupyterhub_config.py .

        echo "c.MultiKernelManager.default_kernel_name='python2'" >> jupyterhub_config.py

        sudo jupyterhub

Consultamos el nodo reservado con **squeue** y accedemos de la siguiente manera:

Guane13 = www.sc3.uis.edu.co/guaneJ13

---

# Instrucciones para inciar el servidor de Digits #

1. Realizar una conexión a Guane

        ssh user@toctoc.grid.uis.edu.co
        ssh user@guane.uis.edu.co

2. Copiar el siguiente script **iniciar_digits.sh** en Guane y dar permisos de ejecución.

        #!/bin/bash

        export PYTHONPATH=/usr/local/caffeDigits/python/caffe/proto:$PYTHONPATH

        /usr/local/digits/digits-devserver -p 5000

3. Realizar una reserva lanzando **srun --gres=gpu:4 iniciar_digits.sh**

4. Enlazar los puertos con el nodo reservado en guane, por ejemplo Guane13

        ssh user@toctoc.grid.uis.edu.co -L 5000:localhost:5000
        ssh user@guane.uis.edu.co -L 5000:guane13:5000

5. En el enlace http://localhost:5000 debería encontrar el servidor de Digits en Guane

**Nota:** Recuerde mantener los terminales con las dos conexiones abiertas.