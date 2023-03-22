# exHExpPred: Exposome HexpPred Module 
### Author: Changxin Lan (lancx_pku@foxmail.com)
### Date: 2023-03-22
HExpPred module is designed  to predict blood concentrations of chemicals and prioritize chemicals of health concern.

Users can install the package using the following code:
```R
if (!requireNamespace("devtools", quietly = TRUE)){

	install.packages("devtools")

	devtools::install_github('ExposomeX/exHExpPred',force = TRUE)
}

library(exHExpPred)
```

### Tips:
&nbsp;&nbsp;&nbsp;&nbsp;1.Before using the package, a user defined physical output path (i.e., OutPath) is recommended. For example
```R
OutPath = "D:/test" #The default path is the current working directory of R. Users can use this code to set the preferred path.
```
&nbsp;&nbsp;&nbsp;&nbsp;2.For each step, the returned values can be named as users' like by following R language requirement.<br>

&nbsp;&nbsp;&nbsp;&nbsp;3.All the PID must be the same with the one provided by InitMedt function, e.g., res$PID.

### Example codes:
#### 1. Initial HExpPred module
```R
res = InitHEP()
res$PID
```
#### 2. Load data for HExpPred analyses
```R
res2 <- LoadHEP(PID=res$PID,
	            UseExample = "example#1",
	            DataPath = NULL)
res2$Expo$Data
```

#### 3. Convert different IDs to the unified ExposomeX IDs
```R
res3 <- ConvToExpoID(PID=res$PID,
                OutPath =OutPath)
res3
```
#### 4. Predict blood concentrations of chemicals
```R
res4 <- PredBlood(PID=res$PID,
                OutPath =OutPath,
                MC = 'F',
                N = 100)
res4$PredBlood$pred_Cb
res4$PredBlood$plot_model_fit
```

#### 5. Visualize the Preddictin results
```R
res5<- VizPredBlood(PID=res$PID,
                OutPath =OutPath,
                Layout = "forest",
                Brightness = "light",
                Palette = "default1")
res5$VizPredBlood$plot_pred
res5$VizPredBlood$ForestPlot
```

#### 6.Exit
```R
FuncExit(PID=res$PID)
```
