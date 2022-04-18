## Jupyter Notebook Overview
Jupyter Notebook is a web application for interactive computing throughout the whole process from development and documentation writing to code execution and result display. For more information, please see [The Jupyter Notebook](https://jupyter-notebook.readthedocs.io/en/latest/notebook.html).

In short, Jupyter Notebook is opened on a webpage where you can directly write and run code, and the code execution result will be directly displayed below the code block. If you need to write help documents during programming, you can write them directly on the same page to describe and explain the code promptly.

### Components
- Web application
A web application is a tool in the form of a webpage that provides help documentation writing, mathematical formulas, interactive computation, and other rich media features. In brief, it is a tool that can implement various features.
- Document
All interactive computations, explanatory text writing, mathematical formulas, images, and other rich media inputs and outputs in Jupyter Notebook are represented as documents. These documents are `JSON` files with the `.ipynb` extension, which facilitate version control and file sharing. In addition, documents can be exported in various formats such as HTML, LaTeX, and PDF.

### Main features of Jupyter Notebook
1. It provides syntax highlighting, indentation, and tab completion for programming.
2. It can run code directly in a browser with the result displayed below the code block.
3. It displays the computation results in rich media formats such as HTML, LaTeX, PNG, and SVG.
4. It supports Markdown syntax for writing of code help documents or statements.
5. It allows you to use LaTex to write code comments containing mathematical notations.

## Installing Jupyter
Enter the EMR [purchase page](https://buy.cloud.tencent.com/emr).
- Select `EMR-V2.3.0` as the product version.
- Select **tensorflowonspark 1.4.4** in the **Optional Component** list, and `Jupyter` will be automatically installed in the `/usr/local/service/jupyter` directory. Jupyter will not start any service. If you have not installed TensorFlowOnSpark, the default installation path will be `/usr/local/service/apps/jupyter`.

## Using Jupyter
### Initializing Jupyter configuration
```
Usage: init.sh [password] [port]
# Sample
./init.sh 123456 10086
```
Press Enter consecutively until the following information is displayed:
```
[hadoop@10 jupyter]$ ./init.sh 123456 10086
Your password is: 123456
Your signature is: sha1:139fa061bae6:bcdc6a7870878458c7c14594fe65dd21f85f84a4
Generating a 4096 bit RSA private key
.............................++
..................................................................................++
writing new private key to '/usr/local/service/jupyter/conf/jkey.key'
-----
You are about to be asked to enter information that will be incorporated
into your certificate request.
What you are about to enter is what is called a Distinguished Name or a DN.
There are quite a few fields but you can leave some blank
For some fields there will be a default value,
If you enter '.', the field will be left blank.
-----
Country Name (2 letter code) [XX]:
State or Province Name (full name) []:
Locality Name (eg, city) [Default City]:
Organization Name (eg, company) [Default Company Ltd]:
Organizational Unit Name (eg, section) []:
Common Name (eg, your name or your server's hostname) []:
Email Address []:
Jupyter config has already generated at /usr/local/service/jupyter/conf/jupyter_notebook_config.py
Now, you can execute the following command to start jupyter:
jupyter notebook --config=/usr/local/service/jupyter/conf/jupyter_notebook_config.py --allow-root
```
At this point, Jupyter configuration has been generated. You can also modify relevant parameters in the generated configuration file `jupyter_notebook_config.py` as instructed on the Jupyter official website.
>!The last row is the startup command. You can copy it to start Jupyter.


### Starting Jupyter Notebook
```
jupyter notebook --config=/usr/local/service/jupyter/conf/jupyter_notebook_config.py --allow-root
[I 10:47:46.972 NotebookApp] Writing notebook server cookie secret to /home/hadoop/.local/share/jupyter/runtime/notebook_cookie_secret
[I 10:47:47.748 NotebookApp] Serving notebooks from local directory: /usr/local/service/jupyter
[I 10:47:47.749 NotebookApp] The Jupyter Notebook is running at:
[I 10:47:47.749 NotebookApp] https://(10.0.0.7 or 127.0.0.1):10086/
[I 10:47:47.749 NotebookApp] Use Control-C to stop this server and shut down all kernels (twice to skip confirmation).
```
### Accessing Jupyter 
Open Jupyter on a webpage (before this operation, you may need to open the Jupyter port in the security group):
```
https://IP:10086/
```
Here, port 10086 is a parameter in the `init.sh` initialization above.
![](https://main.qcloudimg.com/raw/fc370907923fb342b0b27b1fad1f6d2a.png)
You can enter Jupyter's homepage by simply entering the password configured just now.

### Using Jupyter for development
#### **Creating directory**

#### **Renaming directory**
#### **Writing TensorFlow code**
For more information, please visit the [TensorFlow official website](https://github.com/tensorflow/docs/tree/master/site/en/r1/tutorials).

>?You need to download the data set here. The download may be slow in Mainland China.
>
```
import tensorflow as tf

mnist = tf.keras.datasets.mnist

(x_train, y_train),(x_test, y_test) = mnist.load_data()
x_train, x_test = x_train / 255.0, x_test / 255.0

model = tf.keras.models.Sequential([
tf.keras.layers.Flatten(input_shape=(28, 28)),
tf.keras.layers.Dense(512, activation=tf.nn.relu),
tf.keras.layers.Dropout(0.2),
tf.keras.layers.Dense(10, activation=tf.nn.softmax)
])

model.compile(optimizer='adam',
loss='sparse_categorical_crossentropy',
metrics=['accuracy'])

model.fit(x_train, y_train, epochs=5)
model.evaluate(x_test, y_test)
```
#### Running code
Train the model in Jupyter again.
#### Stopping Jupyter service
```
./stop_jupy.sh [jupyter_port]
```

