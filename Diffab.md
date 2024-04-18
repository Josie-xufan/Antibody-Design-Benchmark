# Diffab

### Required Tool

- **env:** 

  ```
  conda activate diffab
  ```

  

- **HDOCK:** design CDRs for antigen without bound antibody framework

  install according to the guidelines

- **PyRosetta:** compute binding energy

  ![image-20240417163456774](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20240417163456774.png)

- **Ray:** 

  install according to the guidelines

- **mmseq:** used for sequence clustering

  ```
  conda install -c conda-forge -c bioconda mmseqs2
  ```

- **pdbfixer:** fixing problems in Protein Data Bank files in preparation for simulating them

  ```
  conda install -c conda-forge pdbfixer
  ```

- **openmm:**  relax the antibody structure

  ```
  conda install -c conda-forge openmm
  ```




### Execute

- ```python
  python design_testset.py
  ```

  针对test set数据集生成CDRs (CDRH1, CDRH2, CDRH3, CDRL1, CDRL2, CDRL3)，每一段CDR都sample100次

  通过设置参数index，选择其中一个test sample进行生成

- ```
  python evaluate.py
  ```

  首先利用openmm以及pyrosetta对生成的structure进行refine

  然后计算IMP，RMSD以及AAR等metrics
  
  

### Result

![image-20240418095751443](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20240418095751443.png)



### Tips

- 采用GitHub上提供的sabdab_summary_all.tsv文件，数据处理部分不会报错。相反若采用自己下载的tsv文件会在sabdab.py line142处报错：https://github.com/luost26/diffab/issues/21

- ```
  ImportError: cannot import name 'COMMON_SAFE_ASCII_CHARACTERS' from 'charset_normalizer.constant'
  pip install chardet
  ```

- ```
  ImportError: /home/****/anaconda3/envs/diffab/lib/python3.8/site-packages/openmm/../../../libstdc++.so.6: version `GLIBCXX_3.4.30' not found
  conda install -c conda-forge libstdcxx-ng
  ```

  