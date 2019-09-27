FROM ubuntu:16.04
RUN apt-get update -y && apt-get install software-properties-common -y && add-apt-repository ppa:deadsnakes/ppa && apt-get update -y && apt-get upgrade -y && apt-get install curl -y
RUN mkdir /home/pipinstall && mkdir /home/flaskapp
RUN cd home/pipinstall && apt-get install python3.6 -y && curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py && python3 get-pip.py
RUN pip install Flask
ENV FLASK_APP app
ENV LC_ALL C.UTF-8
ENV LANG C.UTF-8
EXPOSE 5000
WORKDIR /home/flaskapp
CMD ["flask", "run", "--host", "0.0.0.0"]