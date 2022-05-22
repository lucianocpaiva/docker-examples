FROM python:3.10-slim
RUN apt update -y && apt install -y && apt clean -y

RUN python -m pip install --upgrade pip

RUN pip install --no-cache-dir pandas numpy matplotlib notebook requests lxml pymysql sqlalchemy


# create directory for notebooks
RUN mkdir /notebooks

EXPOSE 8888

# start the jupyter notebook in server mode
CMD ["jupyter","notebook","--ip=0.0.0.0","--port=8888","--no-browser","--allow-root", "--notebook-dir=/notebooks"]

# docker build --rm -t pandas . && docker run -v $(pwd)/data:/notebooks -p 8888:8888 pandas