---
tags: exmodelight, dsl
title: OpenMOLE GUI - ExModeLight
slideOptions:
  theme: 'white'
  transition: 'fade'
 
---
  <style>
    .reveal .slides section {
        font-size: 35px;
        text-align: left;
        color: #666;
    }   
    
    .reveal .slides h2{
        color: #37abc8;
    }
    
    .reveal blockquote {
        margin-top:20px;
        padding: 0 1em;
        color: #999;
        border-left: 0.25em solid #ddd;
        box-shadow:none;
        font-size:35px;
        font-style:normal;
        width:100%;
    }
    
    .reveal a {
    color: #0c2c85;
    }
    
.reveal .slides section img { 
  background: none;
  border: none;
  box-shadow: none;
  display: block;
  margin: 10px auto;
    max-width:100%;
    max-height:100%;
}
    
    .reveal .slides {
         display: block;
  -moz-box-sizing: border-box;
  box-sizing: border-box;
  background: url(https://miniocodimd.openmole.org:443/codimd/uploads/upload_3d8c8d9cf6036122fc2fca8f07dd9ee3.png) no-repeat 100% 100%;
        background-attachment:fixed;
        background-size: 170px auto;
    }
    
    .reveal .slides strong {
        font-weight: bold;
        color: #aa0000;
    }
    
</style>


## A guided tour of the OpenMOLE application

<img src=https://miniocodimd.openmole.org/codimd/uploads/22a560ed-e7bd-433c-bf8f-f4a3936079a5.png style="height:6em;">



---

## Your instance

https://om.exmodelo.org/\<your first name\>

---

## In the documentation

https://openmole.org/GUI.html

---

## New projects

- from sources
- from market
- **from URL** 
  https://nextcloud.openmole.org/s/GpTxoP289TKs7AZ/download

---

## OpenMOLE scripts

*ascript.oms* (OpenMole Script)
editable, executable in the application
syntax highlighting
errors displayed from script
import scripts (import \_file\_.<omfile>._ or import \_parent\_.<omfile>._)

---

## Files

- browse your project files
- sorting options
- filter
- add/copy/delete file/folder
- upload
- refresh

---

## Authentications

- SSH key
- SSH login / password **(use this for CRIANN credentials)**
- EGI certificate

Test your authentications

---

## Plugins

- add a jar plugin

---

## Run a script

- **import Pi computation from Market Place**
- **open Pi.oms**
- **click Run**

---

## Monitor executions

![](https://miniocodimd.openmole.org:443/codimd/uploads/upload_e2e07e5dd43889a6653773e1a926547c.png)

---

## Check results

CSV files can be displayed as raw data / tables or plots

- *scatter* : dimension1 x dimension2 as points
- *SPLOM* : all dimension_i x dimension_j for all selected i,j
- *1 row = 1 plot*  each line is plot as a curve
- *Heatmap* : the whole matrix is plotted as a heatmap

---