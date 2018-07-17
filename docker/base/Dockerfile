FROM resin/raspberrypi3-python:3.6.1

RUN [ "cross-build-start" ]

RUN pip3 install opencv-python opencv-contrib-python --index-url https://www.piwheels.org/simple

RUN [ "cross-build-end" ]
