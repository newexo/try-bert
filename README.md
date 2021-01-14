# Try BERT

This project contains requirements and some instructions that go along with a demo we gave for running TensorFlow on EC2 GPU instance. Time is a river flowing swiftly so if these files have not been updated in more than a year, do not expect that any of this will still work.

Initially we had intended only to demonstrate how to run BERT from TensorFlow Hub with TensorFlow 2.3, but we started having so much fun that we tried also several different NLP tutorials, generative models for images and actor-critic reinforcement learning using OpenAI gym.

This repo does not contain any code since the examples we covered were all from tutorials in TensorFlow documentation.

## Initial configuration

The instance we used was `g3.4xlarge` configured with AMI `Deep Learning AMI (Ubuntu 18.04) Version 38.0 - ami-091b192bc8632b830`. That came with Anaconda Python 3.7. While this meant we could have used `conda` to create an environment, we decided to use a virtual environment wrapper to be compatible with other demonstrations we have done in the past.

After spinning up the instance, `ssh`. Check that GPU is available.

    nvidia-smi

Check python version.

    python -V
    ll $(which python)

### Set up virtual environment

Install virtualenvwrapper.

    pip install virtualenvwrapper

Append the following two lines to `.bashrc`

    export WORKON_HOME=$HOME/.virtualenvs
    source $HOME/anaconda3/bin/virtualenvwrapper.sh

Logout and log back in so that virtualenvwrapper commands will be available. Or

    source ~/.bashrc

Set up a virtual environment.

    mkvirtualenv try-bert
    mkdir repos
    cd repos
    git clone https://github.com/newexo/try-bert.git
    cd try-bert
    pip install -r requirements.txt

From here on, the environment will be available after logging in again.

    workon try-bert
    
### Set up drivers for TensorFlow text examples
 
TensorFlow is compiled against a small range of Cuda library versions. To make RNN examples work we need to make cuda 10.1 the default.
 
    sudo rm /usr/local/cuda
    sudo ln -s /usr/local/cuda-10.1 /usr/local/cuda

### Dependencies for OpenAI gym

Displaying the results of the cart and pole demo require apt installing two things. All other parts of the training work without these.

    sudo apt install xvfb python-opengl
