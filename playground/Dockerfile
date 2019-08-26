FROM tensorflow/tensorflow:latest-py3-jupyter

RUN pip install bokeh seaborn statsmodels pymc3 pygp gpyopt sklearn scikit-image keras\
				scipy pandas nltk gensim opencv-contrib-python-headless pydot xgboost h5py

WORKDIR /playground
CMD ["bash", "-c", "source /etc/bash.bashrc && jupyter notebook --notebook-dir=/playground --ip 0.0.0.0 --no-browser --allow-root"] 