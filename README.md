# my-ColossalChat

Please, following the forth comming commands in order to setup the ColossalChat project on your Debian-based Machine:

First, you need to ensure that you have the `venv` module installed. In Python 3.3 and later, it is included by default. If you need to install it separately, you can do so by running:
   
   ```
   sudo apt-get install python3-venv
   ```
   
## Install

```
conda create -n coati
conda activate coati
conda install cudatoolkit=11.7 -c nvidia
git clone https://github.com/hpcaitech/ColossalAI.git
cd ColossalAI
python3 -m venv venv
source venv/bin/activate
cd applications/Chat
pip install .
```

## Install the Transformers

```
rm -r transformers/
git clone https://github.com/hpcaitech/transformers
cd transformers/
pip install .
cd ../examples
pip install -r requirements.txt
```

## Download Datasets
```
git clone https://github.com/XueFuzhao/InstructionWild.git
cd data
curl -L -o instinwild_en.json 'https://drive.google.com/uc?export=download&id=1qOfrl0RIWgH2_b1rYCEVxjHF3u3Dwqay'
curl -L -o instinwild_ch.json 'https://drive.google.com/uc?export=download&id=1OqfOUWYfrK6riE9erOx-Izp3nItfqz_K'

```
