---
layout: post
title:  "TensorFlow auf dem Jetson Nano"
date:   2020-05-12 09:53:28 +0200
categories: jetson-nano KI
permalink: /tensorflow-jetson-nano
---

Auf Nvidias Jetson-Plattform lassen sich die bekannten Machine Learning-Frameworks wie TensorFlow, PyTorch, Caffee/Caffee2, MXNet und Keras in Form der nativen Vollversionen installieren. In diesem Beitrag wird die Installation des wohl bekanntesten Frameworks, [TensorFlow](https://www.tensorflow.org/) von Google, auf dem Jetson Nano gezeigt.

Die Installation ist in dem PDF-Dokument [Installing  TensorFlow For Jetson Platform](https://docs.nvidia.com/deeplearning/frameworks/pdf/Install-TensorFlow-Jetson-Platform.pdf) beschrieben. Weil alle Mitglieder der Jetson-Familie, also Nano, TX2 und Xavier auf der gleichen Softwareplattform, dem *JetPack* beruhen, läuft die Installation auch für alle gleich ab.

Davon ausgehend, dass die aktuelle Jetpack-Version (derzeit 4.4) installiert ist, sind die folgenden Schritte durchzuführen:

Installieren der erforderlichen Bibliotheken:

    sudo apt-get update
    sudo apt-get install libhdf5-serial-dev hdf5-tools libhdf5-dev zlib1g-dev zip libjpeg8-dev liblapack-dev libblas-dev gfortran

Installieren und Updaten des Paketmanagers pip3:

    sudo apt-get install python3-pip
    sudo pip3 install -U pip testresources setuptools

Installieren diverser Python-Abhängigkeiten:

    sudo pip3 install -U numpy==1.16.1 future==0.17.1 mock==3.0.5 h5py==2.9.0 keras_preprocessing==1.0.5 keras_applications==1.0.8 gast==0.2.2 futures protobuf pybind11

Installieren der aktuellen TensorFlow-Version mittels pip:

    sudo pip3 install --pre --extra-index-url https://developer.download.nvidia.com/compute/redist/jp/v44 tensorflow

Das Ausführen aller Anweisungen benötigt auf dem Nano etwa zwei Stunden. Ob die Installation erfolgreich war, erkennt man daran, dass der Import von TensorFlow in einem Python-Fenster keine Fehler produziert:

![Erfolgreiche Installation von TensorFlow](/images/tensorflow-jetson-nano/tensorflow-jetson-nano.png)

Ist das der Fall, ist TensorFlow einsatzbereit.
