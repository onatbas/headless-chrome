FROM headlesschrome

ADD . /app

RUN mkdir /output
WORKDIR /output

RUN pip install -r /app/requirements.txt

CMD python -m robot /app/test.robot
