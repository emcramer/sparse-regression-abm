# APSA-ASCI-AAPI Joint Meeting 2024

<details>
<summary>Bioprint Sample Preparation</summary>
<img alt="Example workflow for sample bioprint preparation" src="apsa-media/apsa-poster-fig-2.png" width="600px"/>
<p>MC38-H2B-RFP labeled colorectal cancer tumor cells co-cultured with primary bone marrow derived macrophages Y01-Actin-GFP were FACS sorted to isolate double positive RFP-GFP cells</p>
<p>Cells were printed onto collagen-coated plates using a Biopixlar printer with a heated stage insert produced by Fluicell.</p>
</details>

## Example Simulations
Gifs are organized by spatial location of the initial conditions for each simulation and show examples of simulations that differ by the chemotaxis sensitivity of hybrid cells to a simulated cancer secretant.

<details>
<summary>Hybrid Margin, Tumor Core</summary>
<h3 >Example</h3>

| sim-f3c34d11a024be4a10c1a01fde0eb7bc | sim-a32056bd58aa8e988db807474eee0742 | 
|--|--|  
| Cancer substrate sensitivity = 0.94 | Cancer substrate sensitivity = 0.39 |  
| <img src="apsa-media/bioprint-abm-sim-eb7bc-0.94sensitivity-hybrid-margin.gif" width="400px" /> | <img src="apsa-media/sim-a32056bd58aa8e988db807474eee0742-sens0.39-ichybrid-margin.gif" width="400px"/> |  
| <img src="apsa-media/sim-f3c34d11a024be4a10c1a01fde0eb7bc-cancer-ligand-contour.gif" width="400px"> | <img src="apsa-media/sim-a32056bd58aa8e988db807474eee0742-cancer-ligand-contour.gif" width="400px"/>|

</details>

<details>
<summary>Hybrid Core, Tumor Margin</summary>
<h3 >Example</h3>

| sim-5f32272f105002a044f8aa0bbf0a0231 | sim-39c031049a9066f1d9933c99f41c319e | 
|--|--|  
| Cancer substrate sensitivity = 0.80 | Cancer substrate sensitivity = 0.27 |  
| <img src="apsa-media/sim-5f32272f105002a044f8aa0bbf0a0231-sens0.8-ichybrid-core.gif" width="400px" /> | <img src="apsa-media/sim-39c031049a9066f1d9933c99f41c319e-sens0.27-ichybrid-core.gif" width="400px"/> |  
| <img src="apsa-media/sim-5f32272f105002a044f8aa0bbf0a0231-cancer-ligand-contour.gif" width="400px"> | <img src="apsa-media/sim-39c031049a9066f1d9933c99f41c319e-cancer-ligand-contour.gif" width="400px"> |

</details>

## Bioprinting the TME

>Multiplex Single-Cell Bioprinting for Engineering of Heterogeneous Tissue Constructs with Subcellular Spatial Resolution
Haylie R. Helms, Kody A. Oyama, Jason P. Ware, Stuart D. Ibsen, Luiz E. Bertassoni
bioRxiv 2024.02.01.578499; doi: https://doi.org/10.1101/2024.02.01.578499

<img src="apsa-media/helms-et-al-fig-6c.png" width="720px">
Patterned vs random (“co-culture”) prints containing MCF10A, MDA-MB-231, and mammary fibroblasts. Live cell images at 0, 3, and 12 hours. Immunofluorescence staining for pan cytokeratin (PanCK), vimentin (VIM), and nucleus (DAPI). 

### Test Environment for Adapting Bioprints to ABM

<details>
<summary>Hybrid Margin, Tumor Core</summary>
<h3 >Replicate #1</h3>

| Hybrid Margin, Tumor Core | Hybrid Core, Tumor Margin | 
|--|--|   
| <img src="apsa-media/hybrid-4-margin-tumor-core.gif" width="400px" /> | <img src="apsa-media/hybrid-4-core-tumor-margin.gif" width="400px"/> |  

<p>Hybrid cells are joint GFP-RFP fusions of macrophages and colorectal tumor cells. They appear green and yellow on the liver cell imaging. Colorectal tumor cells are RFP positive.</p>

</details>

## Rules for Agent-Based Model
<details>
<summary>Hill Functions</summary>
Commonly used to model substrate concentrations or binding affinity of proteins in biochemistry. In this case, we use it to model a given response to a stimulus (eg. substrate).
A helpful full description of Hill Functions and their parameters <a href="https://www.physiologyweb.com/calculators/hill_equation_interactive_graph.html">here</a>.
<br/>
<img src="apsa-media/Hill-Langmuir_equation.png" width="720px"/>
</details>

<details>
<summary>Rule Set (Development Ongoing)</summary>

| Cell Type | Stimulus               | Effect    | Response                | Saturation | Half-Max | Hill Coefficient |
|-----------|------------------------|-----------|-------------------------|------------|----------|------------------|
| tumor     | pressure               | decreases | cycle entry             | 0          | 1        | 4                |
| tumor     | oxygen                 | increases | cycle entry             | 0.00007    | 21.5     | 2                |
| tumor     | oxygen                 | decreases | necrosis                | 0          | 3.75     | 8                |
| tumor     | dead                   | increases | debris secretion        | 1          | 0.5      | 10               |
| tumor     | oxygen                 | increases | canc_ligand secretion   | 1          | 0.5      | 8                |
| tumor     | hybrid_ligand gradient | increases | migration speed         | 1          | 0.5      | 2                |
| tumor     | hybrid_ligand gradient | increases | migration bias          | 1          | 0.5      | 4                |
| hybrid    | oxygen                 | increases | cycle entry             | 0.00007    | 21.5     | 2                |
| hybrid    | pressure               | decreases | cycle entry             | 0          | 1        | 4                |
| hybrid    | oxygen                 | decreases | necrosis                | 0          | 1        | 4                |
| hybrid    | canc_ligand gradient   | increases | migration speed         | 1          | 0.5      | 2                |
| hybrid    | canc_ligand gradient   | increases | migration bias          | 1          | 0.5      | 4                |
| hybrid    | oxygen                 | increases | hybrid_ligand secretion | 1          | 0.5      | 4                |

</details>