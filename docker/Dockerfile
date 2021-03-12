FROM ros:kinetic

# Basic tools and dependencies and nodejs LTS PPA.
RUN apt update && apt install -y curl && curl -sL https://deb.nodesource.com/setup_8.x | bash -

# Install rvizweb.
WORKDIR /rvizweb_ws
ARG rvizweb_branch=master
RUN git clone https://github.com/sergeant-wizard/rvizweb/ src/rvizweb -b ${rvizweb_branch}
RUN rosdep install --from-paths src --ignore-src -r -y
RUN . /opt/ros/kinetic/setup.sh && catkin_make install

# Clear apt cache.
RUN apt clean

# ENTRYPOINT ["/bin/bash", "-c", "source /rvizweb_ws/install/setup.bash && /bin/bash"]
CMD ["/rvizweb_ws/install/env.sh", "roslaunch", "rvizweb", "rvizweb.launch"]
