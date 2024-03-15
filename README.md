# Supplemental Analyses for ICD-10-GM Crosswalks

[![View Site - on GitHub Pages](https://img.shields.io/badge/View_Site-on_GitHub_Pages-blueviolet?logo=github)]([https://itcr-uni-luebeck.github.io/cross-walk-analysis-icd-10-gm/])

This document provides further statistical analysis related to the cross-version evaluations of ICD-10.


## Table of Contents

1. [Genral](#1-general)

2. [Non-automatic transition](#2-non-automatic-transition)
    * [Forward](#21-forward)
    * [Backward](#22-backward)
3. [Comparison of ICD-10 codes with version 2024](#3-comparision-of-icd-10-codes-with-version-2024)


## 1. General
The German Federal Institute for Drugs and Medical Devices (BfArM) publishes so-called crosswalk tables. The crosswalk tables, in the form of text files, contain information on how a code in two subsequent versions behaves, for example:  
<p align="center">
<span style="color:#1F77B4"> K20 </span> ; <span style="color:#2CA02C"> K20.0 </span> ; <span style="color:#FF7F0E"> X </span> ; <span style="color:#D62728"> A </span>
</p>
<p align="center">
<span style="color:#1F77B4"> K20 </span> ; <span style="color:#2CA02C"> K20.1 </span> ; <span style="color:#FF7F0E"> X </span> ; <span style="color:#D62728"> X </span> 
</p>
<p align="center">
<span style="color:#1F77B4"> T66 </span> ; <span style="color:#2CA02C"> K20.1 </span> ; <span style="color:#FF7F0E"> X </span> ; <span style="color:#D62728"> X </span>
</p>

The first two columns show codes from the older version (blue) and the newer version (green). The remaining columns display transition information: from older to newer version (forward, orange) and from newer to older version (backward, red). An automatic transition is expressed by `A` in the tables. Non-automatic transition is represented by an empty entry in the tables, which, in this work, will be represented by `X` to improve readability. In total, 21 ICD-10-GM versions are considered between the years 2004 and 2024.
Based on the provided [Neo4J database](https://github.com/itcr-uni-luebeck/cross-walk-analysis-icd-10-gm/tree/main/Neo4j%20Database) and ConceptMaps [R4](https://github.com/itcr-uni-luebeck/cross-walk-analysis-icd-10-gm/tree/main/ConceptMap-R4) and [R5](https://github.com/itcr-uni-luebeck/cross-walk-analysis-icd-10-gm/tree/main/ConceptMap-R5) the analysis were carried out.

## 2. Non-automatic transition

Here it was analyzed how many codes cannot be automatically transitioned between two successive versions. In addition, five reasons were identified for the non-automatic transitions. These as well as examples and frequencies are also shown.

### 2.1. Forward

On average across the ICD-10-GM versions of 2004 and 2024, <font color="#FF7F0E">0.89 %</font> or 122 codes per crosswalk table cannot be transited automatically.

<img src="images\non-automatic-transiton\2004-2024-forward.png" style="width:80%; display: block; margin-left: auto; margin-right: auto; margin-bottom: 30px"/>

The following five causes for a non-automatic transition were identified:
<table style="margin-left: auto; margin-right: auto;  margin-bottom: 30px">
    <tr><th> <p style="margin-bottom:-5px">Cause</p> </th><th> <p style="margin-bottom:-5px">Example</p> </th><th> <p style="margin-bottom:-5px">Frequency</p> </th></tr>
    <tr><td> <p style="margin-bottom:-5px"><font color="#1F77B4">&#9632;</font> Refinement</p> </td><td> <p style="margin-bottom:-5px">K20 → K20.1</p> </td><td> <p align="right" style="margin-bottom:-5px">48.48 %</p> </td></tr>
    <tr><td> <p style="margin-bottom:-5px"><font color="#FF7F0E">&#9632;</font> New Codes</p> </td><td> <p style="margin-bottom:-5px">UNDEF → U69.75</p> </td><td> <p align="right" style="margin-bottom:-5px">12.50 %</p> </td></tr>
    <tr><td> <p style="margin-bottom:-5px"><font color="#2CA02C">&#9632;</font> Deleted Codes</p> </td><td> <p style="margin-bottom:-5px">U11.0 → UNDEF</p> </td><td> <p align="right" style="margin-bottom:-5px">0.97 %</p> </td></tr>
    <tr><td> <p style="margin-bottom:-5px"><font color="#9467BD">&#9632;</font> Reorganization</p> </td><td> <p style="margin-bottom:-5px">T86.88 → T86.84</p> </td><td> <p align="right" style="margin-bottom:-5px">33.51 %</p> </td></tr>
    <tr><td> <p style="margin-bottom:-5px"><font color="#D62728">&#9632;</font> Reorganization with chapter change</p> </td><td> <p style="margin-bottom:-5px">T66 → K20.1</p> </td><td> <p align="right" style="margin-bottom:-5px">4.54 %</p> </td></tr>
</table>

The causes and their frequencies per crosswalk table are as follows:

<img src="images\non-automatic-transiton\2004-2024-causes-forward.png" style="width:100%; display: block; margin-left: auto; margin-right: auto; margin-bottom: 30px"/>

Two further examples of reorganization special (with chapter change):
<table style="margin-left: auto; margin-right: auto;  margin-bottom: 30px">
    <tr><th> <p style="margin-bottom:-5px">Version</p> </th><th> <p style="margin-bottom:-5px">Code old</p> </th><th> <p style="margin-bottom:-5px">Name old</p> </th><th> <p style="margin-bottom:-5px">Code new</p> </th><th> <p style="margin-bottom:-5px">Name new</p> </th></tr>
    <tr><td rowspan="2"> <p style="margin-bottom:-5px">2022-2023</p> </td><td rowspan="2"> <p style="margin-bottom:-5px">K20</p> </td><td rowspan="2"> <p style="margin-bottom:-5px">Esophagitis</p> </td><td> <p style="margin-bottom:-5px">K20.1</p> </td><td> <p style="margin-bottom:-5px">Radiogenic esophagitis</p> </td></tr>
    <tr><td><p style="margin-bottom:-5px"><font color="#FF7F0E">T66</font></p></td><td> <p style="margin-bottom:-5px">Radiation sickness, unspecified</p> </td></tr>
    <tr><td rowspan="4"> <p style="margin-bottom:-5px">2016-2017</p> </td><td rowspan="4"> <p style="margin-bottom:-5px">R60.9</p> </td><td rowspan="4"> <p style="margin-bottom:-5px">Oedema, unspecified</p> </td><td> <p style="margin-bottom:-5px"><font color="#FF7F0E">E88.20</font></p> </td><td> <p style="margin-bottom:-5px">Lipoedema, stage I</p> </td></tr>
    <tr><td><p style="margin-bottom:-5px"><font color="#FF7F0E">E88.21</font></p></td><td> <p style="margin-bottom:-5px">Lipoedema, stage II</p> </td></tr>
    <tr><td><p style="margin-bottom:-5px"><font color="#FF7F0E">E88.22</font></p></td><td> <p style="margin-bottom:-5px">Lipoedema, stage III</p> </td></tr>
    <tr><td><p style="margin-bottom:-5px"><font color="#FF7F0E">E88.28</font></p></td><td> <p style="margin-bottom:-5px">Other and unspecified lipoedema</p> </td></tr>
</table>

### 2.2. Backward

On average across the ICD-10-GM versions of 2004 and 2024, <font color="#FF7F0E">0.48 %</font> or 66 codes per crosswalk table cannot be transited automatically.

<img src="images\non-automatic-transiton\2004-2024-backward.png" style="width:80%; display: block; margin-left: auto; margin-right: auto; margin-bottom: 30px"/>

The following five causes for a non-automatic transition were identified:
<table style="margin-left: auto; margin-right: auto;  margin-bottom: 30px">
    <tr><th> <p style="margin-bottom:-5px">Cause</p> </th><th> <p style="margin-bottom:-5px">Example</p> </th><th> <p style="margin-bottom:-5px">Frequency</p> </th></tr>
    <tr><td> <p style="margin-bottom:-5px"><font color="#1F77B4">&#9632;</font> Coarsening</p> </td><td> <p style="margin-bottom:-5px">K20.1 → K20</p> </td><td> <p align="right" style="margin-bottom:-5px">6.46 %</p> </td></tr>
    <tr><td> <p style="margin-bottom:-5px"><font color="#FF7F0E">&#9632;</font> New Codes</p> </td><td> <p style="margin-bottom:-5px">UNDEF → U11.0</p> </td><td> <p align="right" style="margin-bottom:-5px">4.11 %</p> </td></tr>
    <tr><td> <p style="margin-bottom:-5px"><font color="#2CA02C">&#9632;</font> Deleted Codes</p> </td><td> <p style="margin-bottom:-5px">U69.75 → UNDEF</p> </td><td> <p align="right" style="margin-bottom:-5px">36.73 %</p> </td></tr>
    <tr><td> <p style="margin-bottom:-5px"><font color="#9467BD">&#9632;</font> Reorganization</p> </td><td> <p style="margin-bottom:-5px">T86.84 → T86.88 </p> </td><td> <p align="right" style="margin-bottom:-5px">46.31 %</p> </td></tr>
    <tr><td> <p style="margin-bottom:-5px"><font color="#D62728">&#9632;</font> Reorganization with chapter change</p> </td><td> <p style="margin-bottom:-5px">K20.1 → T66</p> </td><td> <p align="right" style="margin-bottom:-5px">6.36 %</p> </td></tr>
</table>

The causes and their frequencies per crosswalk table are as follows:

<img src="images\non-automatic-transiton\2004-2024-causes-backward.png" style="width:100%; display: block; margin-left: auto; margin-right: auto; margin-bottom: 30px"/>

Two further examples of reorganization special (with chapter change):
<table style="margin-left: auto; margin-right: auto;  margin-bottom: 30px">
    <tr>
        <th> <p style="margin-bottom:-5px">Version</p> </th>
        <th> <p style="margin-bottom:-5px">Code new</p> </th>
        <th> <p style="margin-bottom:-5px">Name new</p> </th>
        <th> <p style="margin-bottom:-5px">Code old</p> </th>
        <th> <p style="margin-bottom:-5px">Name old</p> </th>
    </tr>
    <tr>
        <td rowspan="2"> <p style="margin-bottom:-5px">2023-2022</p> </td>
        <td rowspan="2"> <p style="margin-bottom:-5px">K20.1</p> </td>
        <td rowspan="2"> <p style="margin-bottom:-5px">Radiogenic esophagitis</p> </td>
        <td> <p style="margin-bottom:-5px">K20</p> </td><td> <p style="margin-bottom:-5px">Esophagitis</p></td>
    </tr>
    <tr>
        <td> <p style="margin-bottom:-5px"><font color="#FF7F0E">T66</font></p> </td><td> <p style="margin-bottom:-5px">Radiogenic esophagitis</p></td>
    </tr>
    <tr>
        <td rowspan="5"> <p style="margin-bottom:-5px">2019-2018</p> </td>
        <td rowspan="5"> <p style="margin-bottom:-5px">G90.70</p> </td>
        <td rowspan="5"> <p style="margin-bottom:-5px">Complex regional pain <br>syndrome of upper limb, other <br>and unspecified type</p> </td>
        <td> <p style="margin-bottom:-5px"><font color="#FF7F0E">M79.60</font></p> </td>
        <td> <p style="margin-bottom:-5px">Pain in limb Multiple sites</p> </td>
    </tr>
    <tr>
        <td><p style="margin-bottom:-5px"><font color="#FF7F0E">M79.61</font></p></td>
        <td> <p style="margin-bottom:-5px">Pain in limb Shoulder region</p> </td>
    </tr>
    <tr>
        <td><p style="margin-bottom:-5px"><font color="#FF7F0E">M79.62</font></p></td>
        <td> <p style="margin-bottom:-5px">Pain in limb Upper arm</p> </td>
    </tr>
    <tr>
        <td><p style="margin-bottom:-5px"><font color="#FF7F0E">M79.63</font></p></td>
        <td> <p style="margin-bottom:-5px">Pain in limb Forearm</p> </td>
    </tr>
    <tr>
        <td><p style="margin-bottom:-5px"><font color="#FF7F0E">M79.64</font></p></td>
        <td> <p style="margin-bottom:-5px">Pain in limb Hand</p> </td>
    </tr>
</table>

## 3. Comparison of ICD-10 codes with version 2024

In the following section, the ICD-10 codes of the previous versions will be compared with those of the version 2024. This involves checking whether the codes of individual annual versions are still terminating in the version of 2024 or whether they still exist.
In summary, the analysis yielded the following average results for the versions considered from 2004 to 2023:
* Still terminating in version 2024: <font color="#FF7F0E">98.48 %</font> (13,279 codes)
* No longer terminating in version 2024: <font color="#FF7F0E">0.89 %</font> (119 codes)
* No longer existing codes in version 2024: <font color="#FF7F0E">0.63 %</font> (84 codes).

The results for the individual annual versions are as follows:

<img src="images\comparison-of-icd-10-codes-with-version-2024\2004-2024-comparision-all-versions.png" style="width:100%; display: block; margin-left: auto; margin-right: auto; margin-bottom: 30px"/>

Two examples of codes of version 2023 that can no longer terminating in version 2024:

<table style="margin-left: auto; margin-right: auto;  margin-bottom: 30px">
    <tr>
        <th> <p style="margin-bottom:-5px">Code (2023)</p> </th>
        <th> <p style="margin-bottom:-5px">Name (2023)</p> </th>
        <th> <p style="margin-bottom:-5px">Code (2024)</p> </th>
        <th> <p style="margin-bottom:-5px">Name (2024)</p> </th>
         <th> <p style="margin-bottom:-5px">Explanation</p> </th>
    </tr>
    <tr>
        <td rowspan="2"> <p style="margin-bottom:-5px">B18.8</p> </td>
        <td rowspan="2"> <p style="margin-bottom:-5px">Other chronic viral <br>hepatitis</p> </td>
        <td> <p style="margin-bottom:-5px">B18.8<font color="#FF7F0E">0</font></p> </td>
        <td> <p style="margin-bottom:-5px">Chronic viral hepatitis E</p></td>
        <td rowspan="2"> <p style="margin-bottom:-5px">The code in the 2024 <br>version has been <br>refined by adding <br>a 5th digit.</p> </td>
    </tr>
    <tr>
        <td> <p style="margin-bottom:-5px">B18.8<font color="#FF7F0E">8</font></p> </td><td> <p style="margin-bottom:-5px">Other chronic viral hepatitis</p></td>
    </tr>
    <tr>
        <td rowspan="6"> <p style="margin-bottom:-5px">S02.4</p> </td>
        <td rowspan="6"> <p style="margin-bottom:-5px">Fracture of malar <br>and maxillary bones</p> </td>
        <td> <p style="margin-bottom:-5px">S02.4<font color="#FF7F0E">0</font></p> </td>
        <td> <p style="margin-bottom:-5px">Fracture of malar, maxillary and zygoma bones, unspecified</p></td>
        <td rowspan="6"> <p style="margin-bottom:-5px">The code in the 2024 <br>version has been <br>refined by adding <br>a 5th digit.</p> </td>
    </tr>
    <tr>
        <td> <p style="margin-bottom:-5px">S02.4<font color="#FF7F0E">2</font></p> </td><td> <p style="margin-bottom:-5px">Fracture of alveolus of maxilla</p></td>
    </tr>
    <tr>
        <td> <p style="margin-bottom:-5px">S02.4<font color="#FF7F0E">3</font></p> </td><td> <p style="margin-bottom:-5px">Unspecified severe protein-energy malnutrition</p></td>
    </tr>
    <tr>
        <td> <p style="margin-bottom:-5px">S02.4<font color="#FF7F0E">8</font></p> </td><td> <p style="margin-bottom:-5px">Malignant neoplasm: peritoneum, unspecified</p></td>
    </tr>
    <tr>
        <td> <p style="margin-bottom:-5px">S02.4<font color="#FF7F0E">9</font></p> </td><td> <p style="margin-bottom:-5px">Fracture of the zygomatic bone and maxilla: multiple parts</p></td>
    </tr>
</table>


