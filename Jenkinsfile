//Scripted Pipeline
node ('agent1') {

		stage('Git_Clone'){
		    git branch: 'dev', 
            credentialsId: '', 
            url: 'git@github.com:Jammi-UwU-Jammy/jens.git'
		}
		

        // Requires MATLAB plugin
		stage('Pipeline Generation'){
            
            env.PATH = "/home/omgisthisdevich/MATLAB/R2025b/bin/matlab"
            
            /* Open the project and generate the pipeline using
            appropriate options */

            runMATLABCommand '''cp = openProject(pwd);
            padv.pipeline.generatePipeline(...
            padv.pipeline.JenkinsOptions(...
            PipelineArchitecture = padv.pipeline.Architecture.SerialStagesGroupPerTask,...
            GeneratorVersion = 1, ...
            GeneratedJenkinsFileName = "simulink_pipeline",...
            GeneratedPipelineDirectory = fullfile("derived","pipeline")));'''
		}

        
        // pass necessary environment variables to generated pipeline
		withEnv(["PATH=/home/omgisthisdevich/MATLAB/R2025b/bin:${env.PATH}"]) {        // Linux
			
            def rootDir = pwd()
            
            /* This file is generated automatically by 
            padv.pipeline.generatePipeline with a default name 
            of simulink_pipeline. Update this field if the 
            name or location of the generated pipeline file is changed */

			load "${rootDir}/derived/pipeline/simulink_pipeline"  
		}
}
