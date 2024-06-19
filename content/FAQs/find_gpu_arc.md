---
title: Find the NVIDIA GPU architecture
---
1. Go the the terminal and type `nvidia-smi`
2. The output will look like this:

```bash
+-----------------------------------------------------------------------------+
| NVIDIA-SMI 515.xx.xx    Driver Version: 515.xx.07    CUDA Version: 11.7     |
|-------------------------------+----------------------+----------------------+
| GPU  Name        Persistence-M| Bus-Id        Disp.A | Volatile Uncorr. ECC |
| Fan  Temp  Perf  Pwr:Usage/Cap|         Memory-Usage | GPU-Util  Compute M. |
|                               |                      |               MIG M. |
|===============================+======================+======================|
|   0  Quadro P1000        Off  | 00000000:01:00.0  On |                  N/A |
| 34%   41C    P8    N/A /  N/A |    299MiB /  4096MiB |      0%      Default |
|                               |                      |                  N/A |
+-------------------------------+----------------------+----------------------+
```
3. From the output, you can see that the GPU is **Quadro P1000**. Now, go to the [NVIDIA website](https://developer.nvidia.com/cuda-gpus) and find the GPU **Compute Capability**. In this case, the compute capability is **6.1**.

4. Each major version of Compute Capability has a corresponding **architecture**. This table
gives the mapping between the Compute Capability and the architecture:

| Compute Capability | Architecture |
|--------------------|--------------|
| 5.x                | Maxwell      |
| 6.x                | Pascal       |
| 7.x                | Volta        |
| 7.5                | Turing       |
| 8.x                | Ampere       |
| 8.9                | Ada          |
| 9.x                | Hopper       |
| 10.x               | Balackwell   |

Since NVIDIA changes the link to the GPU architecture documentation, it's difficult to provide a direct link where you can find the above information. However, look here for more
information:

[Compute Capabilities](https://docs.nvidia.com/cuda/cuda-c-programming-guide/index.html#compute-capabilities)

[CUDA Wikipedia](https://en.wikipedia.org/wiki/CUDA)


5. Therefore, for this GPU, the architecture is **Pascal** and the CUDA capability is **6.1**. And for pcms, you will write `PASCAL61`.

