### Try BERT

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

Install virtualenvwrapper.

    pip install virtualenvwrapper

Append the following two lines to `.bashrc`

    export WORKON_HOME=$HOME/.virtualenvs
    source $HOME/anaconda3/bin/virtualenvwrapper.sh

Logout and log back in so that virtualenvwrapper commands will be available.

Set up a virtual environment.

    mkvirtualenv try-bert
    mkdir repos
    cd repos
    git clone https://github.com/newexo/try-bert.git
    cd try-bert
    pip install -r reqirements.txt

From here on, the environment will be available after logging in again.

    workon try-bert