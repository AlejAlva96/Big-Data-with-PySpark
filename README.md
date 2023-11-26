## Getting Started

### 1. Install Java and Wget:

Spark requires the Java Runtime Environment (JRE) to run. If you don't already have Java installed, you can do it using `apt`:

```bash
sudo apt update
sudo apt install -y wget openjdk-11-jre-headless
```

Set the `JAVA_HOME` environment variable to the path where Java is installed:

```bash
echo "export JAVA_HOME=/usr/lib/jvm/java-11-openjdk-amd64" >> ~/.bashrc
source ~/.bashrc
```

### 2. Install Conda:

To run the notebooks, we will use a Conda environment. Execute the following commands that will download the Linux installer from the [official site](https://www.anaconda.com/download/) and install it:

```bash
wget https://repo.anaconda.com/archive/Anaconda3-2023.07-2-Linux-x86_64.sh
chmod +x Anaconda3-*-Linux-x86_64.sh
./Anaconda3-*-Linux-x86_64.sh
rm Anaconda3-*-Linux-x86_64.sh
```

Follow the prompts on the installer and accept the default settings. When finished, close and re-open your terminal window.

### 3. Create a Conda Environment:
 
Once Conda is installed, create a new environment for the course with the following command:

```bash
conda create -n pyspark python=3.8
```

Activate the created environment:

```bash
conda activate pyspark
```

### 4. Install PySpark and Required Libraries:

With the pyspark environment activated, install PySpark and other required libraries:

```bash
pip install pyspark jupyter jupyterlab
```

### 5. Start Jupyter:

Navigate to the notebooks folder and start Jupyter notebook with:

```bash
cd notebooks/
jupyter lab
```

### Evitar error de PySpark Java Error

Después de esto, es posible que tengamos errores de Java cuando ejecutemos nuestros códigos de PySpark. Para ello tendremos que hacer lo siguiente:

```bash
conda install -c cyclus java-jdk
```

Si al ejecutar ese comando obtenemos un error de Conda SSL Error: OpenSSL Appears to Be Unavailable on This Machine Anaconda, haremos lo siguiente:
1.	Vamos a c:/users/<miusuario>/Anaconda3/Library/bin/ y copiamos los ficheros siguientes: libcrypto-1_1-x64.dll y libssl-1_1-x64.dll.
2.	Los copiamos en el directorio c:/users/<miusuario>/Anaconda3/DLLs.
Depués de esto, tratamos de ejecutar de nuevo el comando: conda install -c cyclus java-jdk
Si tras esto, seguimos obteniendo el mismo error, instalaremos findspark:
```bash
conda install -c conda-forge findspark
```

### Iniciamos PySpark en nuestro script
```bash
import findspark
findspark.init()
```

Creamos sesión PySpark

```bash
from pyspark.sql import SparkSession
spark = SparkSession.builder \
            .appName("Spark Alex") \
            .getOrCreate()
```

