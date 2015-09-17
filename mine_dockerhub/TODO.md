python2-development-base:
    - Dockerfile:
        - Configure vim and tmux from my "dot_files" github repository.
    - Commit as a new image and push to DockerHub

python2-datascience-playground:
    - Dockerfile:
        - Base it on the image "python2-development-base" above
        - Remove the first part of the Dockerfile (the instructions are already
          at "python2-development-base")
        - Auto-start the ipython notebook ("ENTRYPOINT")
    - Commit as a new image and push to DockerHub
