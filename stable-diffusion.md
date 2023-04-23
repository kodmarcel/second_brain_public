---  
share: true  
tag: public  
---  
scr# Installation on fedora  
```  
sudo dnf install conda  
conda init bash  
git clone https://github.com/Stability-AI/stablediffusion  
cd stablediffusion  
conda env create -f environment.yaml  
conda activate ldm      
pip install -e .  
```  
  
## For GPU optimization run:  
*run while having ldm activated from previous step!*  
```  
xport CUDA_HOME=/usr/local/cuda-11.4  
conda install -c nvidia/label/cuda-11.4.0 cuda-nvcc  
conda install -c conda-forge gcc  
conda install -c conda-forge gxx_linux-64==9.5.0  
cd ..  
git clone https://github.com/facebookresearch/xformers.git  
cd xformers  
git submodule update --init --recursive  
pip install -r requirements.txt  
pip install -e .  
cd ../stablediffusion  
```  
  
download ckpt file from  [huggingface](https://huggingface.co/stabilityai/stable-diffusion-2-1)  
  
  
```  
python scripts/txt2img.py --prompt "a professional photograph of an astronaut riding a horse" --ckpt v2-1_512-ema-pruned.ckpt --config v2-1_512-ema-pruned.yaml --H 768 --W 768   
```  
  
python scripts/txt2img.py --prompt "YOUR-PROMPT-HERE" --plms --ckpt sd-v1-4.ckpt --skip_grid --n_samples 1  
