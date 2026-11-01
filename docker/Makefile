.PHONY: all \
        px4-dev-simulation-ubuntu24 \
        uavros2

# Default: build the Ubuntu 24 / ROS 2 Jazzy image.
all: px4-dev-simulation-ubuntu24

# ---------- Ubuntu 24 / ROS 2 Jazzy ----------
# Tagged with the bare name docker_run.sh and docker-compose.yml start.
px4-dev-simulation-ubuntu24:
	docker build -t px4-dev-simulation-ubuntu24 . -f Dockerfile_simulation-ubuntu24

# ---------- Ready-to-run uavros2 (PX4 SITL + workspace built; needs the image above) ----------
# Override the refs with e.g. `make uavros2 UAVROS2_REF=my-branch`.
PX4_REF ?= v1.15.4
UAVROS2_REF ?= main
uavros2: px4-dev-simulation-ubuntu24
	docker build -t uavros2:jazzy . -f Dockerfile_uavros2 \
		--build-arg PX4_REF=$(PX4_REF) --build-arg UAVROS2_REF=$(UAVROS2_REF)
