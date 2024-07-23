# BBTools Docker Container

This repository contains Dockerfile and Singularity files to create an image of the BBTools. BBTools is a suite of bioinformatics tools designed for handling and analyzing biological sequences.

## Prerequisites

- [Docker](https://www.docker.com/get-started) installed on your machine.
- [Apptainer](https://apptainer.org ) installed on your machine.

## Building the Docker Image

1. Clone this repository or download the Dockerfile.
2. Navigate to the directory containing the Dockerfile.
3. Build the Docker image with the following command:

   ```sh
   #docker
   docker build -t bbtools-container .

   # singularity
   singularity build bbtools_v39.08.sif singularity_bbtools_v39.08.def

   ```

## Running the Docker Container

To run the Docker container in interactive mode:

```sh
docker run -it --rm bbtools-container

module load singularity/current
singularuty run bbtools_v39.08.sif
```

This command will start the container and open a bash shell.

### Mounting Volumes

If you need to access data from your host machine, you can mount a directory as a volume. For example:

```sh
docker run -it --rm -v /path/to/local/data:/data bbtools-container
```

This mounts the local directory `/path/to/local/data` to `/data` inside the container.

## Using BBTools

Once inside the container, you can use BBTools commands. For example:

```sh
reformat.sh in=input.fastq out=output.fastq

# Just adapter trimming
singularity run bbtools_v39.08.sif bbduk.sh in1=<input-pair1> in2=<input-pair2> out1=<trimmed-pair1> out2=<trimmed-pair2> ref=<path/to/resources/adapters.fa> ktrim=r k=23 mink=11 hdist=1 tpe tbo
# Quality filtering
singularity run bbtools_v39.08.sif bbduk.sh in1=<trimmed-pair1> in2=<trimmed-pair2> qtrim=rl trimq=10 out1=<trimmed-and-quality-pair1> out2=<trimmed-and-quality-pair2>
```

Replace `input.fastq` and `output.fastq` with your actual file names.

## Additional Information

- [BBTools Documentation](https://jgi.doe.gov/data-and-tools/software-tools/bbtools/)

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.
