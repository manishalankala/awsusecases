



Using MNIST dataset

# Files


CNN_code.py

```
#!/usr/bin/env python
# coding: utf-8

# In[ ]:


import yaml
from datetime import datetime
from keras.datasets import mnist
from keras.models import Sequential
from keras.layers import Dense
from keras.utils import np_utils
import numpy as np
def yaml1(i):
    with open('Adding_layer.yaml') as f:
    
        docs = yaml.load_all(f, Loader=yaml.FullLoader)
    
        for doc in docs:
            
            for key, value in doc.items():
                valu = value[0:i]	
    return valu
# loading data & Layers
def modeltrain(num_classes,num_pixels,i):
    model = Sequential()
    model.add(Dense(num_pixels, input_dim=num_pixels, kernel_initializer='normal', activation='relu'))
    model.add(Dense(num_classes, kernel_initializer='normal', activation='relu'))
    value=yaml1(i)
    for i in value:
        exec(i)
    model.compile(loss='categorical_crossentropy', optimizer='adam', metrics=['accuracy'])
    model.summary()
    return model
def loaddata():
    (X_train, y_train), (X_test, y_test) = mnist.load_data()
    num_pixels = X_train.shape[1] * X_train.shape[2]
    X_train = X_train.reshape((X_train.shape[0], num_pixels)).astype('float32')
    X_test = X_test.reshape((X_test.shape[0], num_pixels)).astype('float32')
    X_train = X_train / 255
    X_test = X_test / 255
    y_train = np_utils.to_categorical(y_train)
    y_test = np_utils.to_categorical(y_test)
    num_classes = y_test.shape[1]
    i=0
    for i in range(5):
        model=modeltrain(num_classes,num_pixels,i)
        model.fit(X_train, y_train, validation_data=(X_test, y_test), epochs=5, batch_size=200, verbose=2)
        scores = model.evaluate(X_test, y_test, verbose=1)
        test_loss, test_acc = model.evaluate(X_test, y_test)
        print('Test_loss', test_loss)
        print('Test_accuracy', test_acc)
        with open('Output.txt', 'a') as f:
            now = datetime.now()
            dt_string = now.strftime("%d/%m/%Y %H:%M:%S")
            print("Date and Time:",dt_string,file=f)	
            print("Accuracy:",test_acc, file=f)
            f.close()
        if test_acc < 0.95:
            continue
        else:
            break


loaddata()
 


# In[ ]:


```



mail.py

```
#!/usr/bin/env python
# coding: utf-8

# In[13]:


import smtplib
from email.mime.text import MIMEText
from email.mime.multipart import MIMEMultipart
from email.mime.base import MIMEBase
from email import encoders
import os.path

email = 'Sender email'
password = 'Sender email password'
send_to_email = 'rajpurohitprakash@gmail.com'
subject = 'Model Accuracy'
message = "Hey Developer!!! Check your final Model Accuracy after all tweaking. Now your model is giving desired accuracy."
file_location = 'Output.txt'

msg = MIMEMultipart()
msg['From'] = email
msg['To'] = send_to_email
msg['Subject'] = subject

msg.attach(MIMEText(message, 'plain'))

# Setup the attachment
filename = os.path.basename(file_location)
attachment = open(file_location, "rb")
part = MIMEBase('application', 'octet-stream')
part.set_payload(attachment.read())
encoders.encode_base64(part)
part.add_header('Content-Disposition', "attachment; filename= %s" % filename)

# Attach the attachment to the MIMEMultipart object
msg.attach(part)

server = smtplib.SMTP('smtp.gmail.com', 587)
server.starttls()
server.login(email, password)
text = msg.as_string()
server.sendmail(email, send_to_email, text)
server.quit()


# In[ ]:


```













Dockerfile

```
FROM centos

RUN yum install python36 -y

RUN yum install epel-release -y
RUN yum update -y

RUN curl "https://bootstrap.pypa.io/get-pip.py" -o "get-pip.py"
RUN python3 get-pip.py

RUN pip install setuptools
RUN pip install keras
RUN pip install pillow
RUN pip install scikit-learn
RUN pip install matplotlib
RUN pip install seaborn
RUN pip install pandas
RUN pip install opencv-python
RUN pip3 install tensorflow
RUN pip install pyyaml

COPY CNN_code.py .
COPY Adding_layers.yaml .
COPY Mail.py .


```


When developer push repository to Github. Jenkins Pull the Github repository automatically in Jenkins workspace and copy that in base OS system.

item ---> scm ---> Repository url github ----. Branch specifier Master ---- Poll scm  ---> build  sudo cp -vrf * /root/data ----> run Job

Build triggers ---> Trigger only if build is stable  ---> Build sudo docker build -t keras:v1 /root/data









