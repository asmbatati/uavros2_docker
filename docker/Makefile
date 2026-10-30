.PHONY: all \
        px4-dev-simulation-ubuntu24 \
        uavros2 \
        px4-dev-simulation-ubuntu22 \
        px4-dev-simulation-jammy \
        px4-simulation-cuda11.7.1-ubuntu22 \
        px4-simulation-cuda12.2.0-ubuntu22 \
        px4.simulation.ubuntu22.wsl

# Default: build the Ubuntu 24 / ROS 2 Jazzy image (this repo's primary target).
all: px4-dev-simulation-ubuntu24

# ---------- Ubuntu 24 / ROS 2 Jazzy (primary) ----------
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

# ---------- Ubuntu 22 / ROS 2 Humble (ported from gps_denied_navigation_docker) ----------
px4-dev-simulation-ubuntu22:
	docker build -t mzahana/px4-dev-simulation-ubuntu22 . -f Dockerfile_simulation-ubuntu22

# ---------- Ubuntu 22 Jammy + ROS 1 (legacy) ----------
px4-dev-simulation-jammy:
	docker build -t mzahana/px4-dev-simulation-jammy . -f Dockerfile_simulation-jammy

# ---------- CUDA variants on Ubuntu 22 / Humble ----------
px4-simulation-cuda11.7.1-ubuntu22:
	docker build -t mzahana/px4-simulation-cuda11.7.1-ubuntu22 . -f Dockerfile_simulation-cuda11.7.1-ubuntu22

px4-simulation-cuda12.2.0-ubuntu22:
	docker build -t mzahana/px4-simulation-cuda12.2.0-ubuntu22 . -f Dockerfile_simulation-cuda12.2.0-ubuntu22

# ---------- WSL-tuned image ----------
px4.simulation.ubuntu22.wsl:
	docker build -t mzahana/px4.simulation.ubuntu22.wsl . -f Dockerfile.ros_humble.ubuntu22.wsl
