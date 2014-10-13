

This is the model of IL13 induced signalling in L1236 cells described in the
article:  
**Dynamic Mathematical Modeling of IL13-Induced Signaling in Hodgkin and Primary Mediastinal B-Cell Lymphoma Allows Prediction of Therapeutic Targets.**   
Raia V, Schilling M, Böhm M, Hahn B, Kowarsch A, Raue A, Sticht C, Bohl S,
Saile M, Möller P, Gretz N, Timmer J, Theis F, Lehmann WD, Lichter P and
Klingmüller U. Cancer Res. 2011 Feb 1;71(3):693-704. PubmedID:
[21127196](http://www.ncbi.nlm.nih.gov/pubmed/21127196) ; DOI: [10.1158/0008-5
472.CAN-10-2987](http://dx.doi.org/10.1158/0008-5472.CAN-10-2987)  
Abstract:  
Primary mediastinal B-cell lymphoma (PMBL) and classical Hodgkin lymphoma
(cHL) share a frequent constitutive activation of JAK (Janus kinase)/STAT
signaling pathway. Because of complex, nonlinear relations within the pathway,
key dynamic properties remained to be identified to predict possible
strategies for intervention. We report the development of dynamic pathway
models based on quantitative data collected on signaling components of
JAK/STAT pathway in two lymphoma-derived cell lines, MedB-1 and L1236,
representative of PMBL and cHL, respectively. We show that the amounts of
STAT5 and STAT6 are higher whereas those of SHP1 are lower in the two lymphoma
cell lines than in normal B cells. Distinctively, L1236 cells harbor more JAK2
and less SHP1 molecules per cell than MedB-1 or control cells. In both
lymphoma cell lines, we observe interleukin-13 (IL13)-induced activation of
IL4 receptor α, JAK2, and STAT5, but not of STAT6. Genome-wide, 11 early and
16 sustained genes are upregulated by IL13 in both lymphoma cell lines.
Specifically, the known STAT-inducible negative regulators CISH and SOCS3 are
upregulated within 2 hours in MedB-1 but not in L1236 cells. On the basis of
this detailed quantitative information, we established two mathematical
models, MedB-1 and L1236 model, able to describe the respective experimental
data. Most of the model parameters are identifiable and therefore the models
are predictive. Sensitivity analysis of the model identifies six possible
therapeutic targets able to reduce gene expression levels in L1236 cells and
three in MedB-1. We experimentally confirm reduction in target gene expression
in response to inhibition of STAT5 phosphorylation, thereby validating one of
the predicted targets.

All concentrations in the model, apart from IL13, are in molecules/cell. IL13
is given in ng/ml. As the cell volume is not explicitely given in the article,
it is just approximately derived from the MW of IL13 (15.8 kDa) and the
conversion factor 3.776 molecules IL13/cell = 1 ng/ml to be around 100 fl.

SBML model exported from PottersWheel on 2010-08-10 12:14:57.  
Inline follows the original matlab code:

    
    
    % PottersWheel model definition file
    
    function m = Raia2010_IL13_L1236()
    
    m             = pwGetEmptyModel();
    
    %% Meta information
    
    m.ID          = 'Raia2010_IL13_L1236';
    m.name        = 'Raia2010_IL13_L1236';
    m.description = '';
    m.authors     = {'Raia et al'};
    m.dates       = {'2010'};
    m.type        = 'PW-2-0-47';
    
    %% X: Dynamic variables
    % m = pwAddX(m, ID, startValue, type, minValue, maxValue, unit, compartment, name, description, typeOfStartValue)
    
    m = pwAddX(m, 'Rec'         ,              1.8, 'fix'   , 1e-006, 10000, 'molecules/cell (x 1000)', 'cell', []  , []  , []             , []  , 'protein.generic');
    m = pwAddX(m, 'Rec_i'       , 118.598421286338, 'global',  0.001, 10000, 'molecules/cell (x 1000)', 'cell', []  , []  , []             , []  , 'protein.generic');
    m = pwAddX(m, 'IL13_Rec'    ,                0, 'fix'   , 1e-006, 10000, 'molecules/cell (x 1000)', 'cell', []  , []  , []             , []  , 'protein.generic');
    m = pwAddX(m, 'p_IL13_Rec'  ,                0, 'fix'   , 1e-006, 10000, 'molecules/cell (x 1000)', 'cell', []  , []  , []             , []  , 'protein.generic');
    m = pwAddX(m, 'p_IL13_Rec_i',                0, 'fix'   , 1e-006, 10000, 'molecules/cell (x 1000)', 'cell', []  , []  , []             , []  , 'protein.generic');
    m = pwAddX(m, 'JAK2'        ,               24, 'fix'   , 1e-006, 10000, 'molecules/cell (x 1000)', 'cell', []  , []  , []             , []  , 'protein.generic');
    m = pwAddX(m, 'pJAK2'       ,                0, 'fix'   , 1e-006, 10000, 'molecules/cell (x 1000)', 'cell', []  , []  , []             , []  , 'protein.generic');
    m = pwAddX(m, 'SHP1'        ,              9.4, 'fix'   , 1e-006, 10000, 'molecules/cell (x 1000)', 'cell', []  , []  , []             , []  , 'protein.generic');
    m = pwAddX(m, 'STAT5'       ,              209, 'fix'   , 1e-006, 10000, 'molecules/cell (x 1000)', 'cell', []  , []  , []             , []  , 'protein.generic');
    m = pwAddX(m, 'pSTAT5'      ,                0, 'fix'   , 1e-006, 10000, 'molecules/cell (x 1000)', 'cell', []  , []  , []             , []  , 'protein.generic');
    m = pwAddX(m, 'CD274mRNA'   ,                0, 'fix'   , 1e-006, 10000, 'molecules/cell (x 1000)', 'cell', []  , []  , []             , []  , 'protein.generic');
    
    
    %% R: Reactions
    % m = pwAddR(m, reactants, products, modifiers, type, options, rateSignature, parameters, description, ID, name, fast, compartments, parameterTrunks, designerPropsR, stoichiometry, reversible)
    
    m = pwAddR(m, {'Rec'         }, {'IL13_Rec'    }, {'IL13stimulation'}, 'C' , [] , 'k1 * m1 * r1 * 3.776', {'Kon_IL13Rec'             });
    m = pwAddR(m, {'Rec'         }, {'Rec_i'       }, {                 }, 'MA', [] , []                    , {'Rec_intern'              });
    m = pwAddR(m, {'Rec_i'       }, {'Rec'         }, {                 }, 'MA', [] , []                    , {'Rec_recycle'             });
    m = pwAddR(m, {'IL13_Rec'    }, {'p_IL13_Rec'  }, {'pJAK2'          }, 'E' , [] , []                    , {'Rec_phosphorylation'     });
    m = pwAddR(m, {'JAK2'        }, {'pJAK2'       }, {'IL13_Rec'       }, 'E' , [] , []                    , {'JAK2_phosphorylation'    });
    m = pwAddR(m, {'JAK2'        }, {'pJAK2'       }, {'p_IL13_Rec'     }, 'E' , [] , []                    , {'JAK2_phosphorylation'    });
    m = pwAddR(m, {'p_IL13_Rec'  }, {'p_IL13_Rec_i'}, {                 }, 'MA', [] , []                    , {'pRec_intern'             });
    m = pwAddR(m, {'p_IL13_Rec_i'}, {              }, {                 }, 'MA', [] , []                    , {'pRec_degradation'        });
    m = pwAddR(m, {'pJAK2'       }, {'JAK2'        }, {'SHP1'           }, 'E' , [] , []                    , {'pJAK2_dephosphorylation' });
    m = pwAddR(m, {'STAT5'       }, {'pSTAT5'      }, {'pJAK2'          }, 'E' , [] , []                    , {'STAT5_phosphorylation'   });
    m = pwAddR(m, {'pSTAT5'      }, {'STAT5'       }, {'SHP1'           }, 'E' , [] , []                    , {'pSTAT5_dephosphorylation'});
    m = pwAddR(m, {              }, {'CD274mRNA'   }, {'pSTAT5'         }, 'C' , [] , 'm1*k1'               , {'CD274mRNA_production'    });
    
    
    
    %% C: Compartments
    % m = pwAddC(m, ID, size,  outside, spatialDimensions, name, unit, constant)
    
    m = pwAddC(m, 'cell', 1);
    
    
    %% K: Dynamical parameters
    % m = pwAddK(m, ID, value, type, minValue, maxValue, unit, name, description)
    
    m = pwAddK(m, 'Kon_IL13Rec'             , 0.00174086832237195, 'global', 1e-009, 1000);
    m = pwAddK(m, 'Rec_phosphorylation'     , 9.07540737285078   , 'global', 1e-009, 1000);
    m = pwAddK(m, 'pRec_intern'             , 0.324132341358502  , 'global', 1e-009, 1000);
    m = pwAddK(m, 'pRec_degradation'        , 0.417538218767296  , 'global', 1e-009, 1000);
    m = pwAddK(m, 'Rec_intern'              , 0.259685756311325  , 'global', 1e-009, 1000);
    m = pwAddK(m, 'Rec_recycle'             , 0.00392430355501153, 'global', 1e-009, 1000);
    m = pwAddK(m, 'JAK2_phosphorylation'    , 0.300019047540849  , 'global', 1e-009, 1000);
    m = pwAddK(m, 'pJAK2_dephosphorylation' , 0.0981610557569751 , 'global', 1e-009, 1000);
    m = pwAddK(m, 'STAT5_phosphorylation'   , 0.00426766529531612, 'global', 1e-009, 1000);
    m = pwAddK(m, 'pSTAT5_dephosphorylation', 0.0116388587580445 , 'global', 1e-009, 1000);
    m = pwAddK(m, 'CD274mRNA_production'    , 0.0115927572109515 , 'global', 1e-009, 1000);
    
    
    %% U: Driving input
    % m = pwAddU(m, ID, uType, uTimes, uValues, compartment, name, description, u2Values, alternativeIDs, designerProps)
    
    m = pwAddU(m, 'IL13stimulation', 'steps', [-100 0]  , [0 1]  , [], [], [], [], {}, [], 'protein.generic');
    
    
    %% Default sampling time points
    m.t = 0:1:120;
    
    
    %% Y: Observables
    % m = pwAddY(m, rhs, ID, scalingParameter, errorModel, noiseType, unit, name, description, alternativeIDs, designerProps)
    
    m = pwAddY(m, 'Rec + IL13_Rec + p_IL13_Rec'         , 'RecSurf_obs'  , 'scale_RecSurf'  , '0.1 * y + 0.1 * max(y)');
    m = pwAddY(m, 'IL13_Rec + p_IL13_Rec + p_IL13_Rec_i', 'IL13-cell_obs', 'scale_IL13-cell', '0.15 * y + 0.05 * max(y)');
    m = pwAddY(m, 'p_IL13_Rec + p_IL13_Rec_i'           , 'pIL4Ra_obs'   , 'scale_pIL4Ra'   , '0.10 * y + 0.15 * max(y)');
    m = pwAddY(m, 'pJAK2'                               , 'pJAK2_obs'    , 'scale_pJAK2'    , '0.1 * y + 0.1 * max(y)');
    m = pwAddY(m, 'CD274mRNA'                           , 'CD274mRNA_obs', 'scale_CD274mRNA', '0.1 * y + 0.1 * max(y)');
    m = pwAddY(m, 'pSTAT5'                              , 'pSTAT5_obs'   , 'scale_pSTAT5'   , '0.1 * y + 0.1 * max(y)');
    
    
    %% S: Scaling parameters
    % m = pwAddS(m, ID, value, type, minValue, maxValue, unit, name, description)
    
    m = pwAddS(m, 'scale_pJAK2'    , 0.469836894150194, 'global',  0.001, 10000);
    m = pwAddS(m, 'scale_pIL4Ra'   ,  1.80002942264669, 'global',  0.001, 10000);
    m = pwAddS(m, 'scale_RecSurf'  ,                 1,    'fix', 0.0001, 10000);
    m = pwAddS(m, 'scale_IL13-cell',  174.726805005048, 'global',  0.001, 10000);
    m = pwAddS(m, 'scale_CD274mRNA', 0.110568221201943, 'global',  0.001, 10000);
    m = pwAddS(m, 'scale_pSTAT5'   ,                 1,    'fix',  0.001, 10000);
    
    
    %% Designer properties (do not modify)
    m.designerPropsM = [1 1 1 0 0 0 400 250 600 400 1 1 1 0 0 0 0];

