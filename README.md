# Fuzzing the Google Closure Compiler with JQF (+Zest for coverage guidance.)
## Fuzzing
We're using the JQF Maven Plugin, which makes fuzzing simpler. There's no installation required. As you can tell, our repository is relatively clean.

To fuzz the Google Closure Compiler, you can first clone or download this repository.
Then, open a terminal in the local directory where this repository is in.

Compile the test driver
`mvn test-compile`

Start fuzzing with 
`mvn jqf:fuzz -Dclass=CompilerTest -Dmethod=testWithGenerator -Dtime=5m`

Replicate failures using <br> 
`mvn jqf:repro -Dclass=CompilerTest -Dmethod=testWithPrintInput -Dinput=target/fuzz-results/CompilerTest/testWithGenerator/failures/id_000000`

The commands above are concrete, the generalized versions are: <br>
`mvn jqf:fuzz -Dclass=<fully-qualified-class-name> -Dmethod=<method-name> -Dtime=<duration> `

`mvn jqf:repro -Dclass=<fully-qualified-class-name> -Dmethod=<method-name> -Dinput=<file-or-directory-name>`

You can also find this info at: https://github.com/rohanpadhye/JQF/wiki/JQF-Maven-Plugin

## Experimental Data
The raw data is in some of the other branches (not main), but since GitHub isn't the best place to store these data... <br>
We recommend you visit this folder instead: https://drive.google.com/file/d/16PWskUDITqvB9_Rl4wDzfbYsIpa_WPLG/view?usp=sharing <br>
Which contains our 2 sets of test results in zip files. There is also a 'data_visuals_files' folder which contains some of the data that we analyzed and some graphs we genereated. 

## Trophies?
If you have noticed, our repo has a `trophies` folder. This contains some of the rarer error-inducing inputs; which is basically everything except null pointer exceptions. <br>
If you would like to see an input that leads to a null pointer exception... look in any non-empty 'failures' folder in our test results and you'll almost certainly find one.

