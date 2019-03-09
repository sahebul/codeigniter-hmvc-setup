In this example i have setup the hmvc extension to codeigniter application. You have simply download and use it.

Please follow following steps if want to HMVC stepup your application.  

Step 1. Download latest ci from https://www.codeigniter.com/

Step 2. Download hmvc extensions from https://bitbucket.org/wiredesignz/codeigniter-modular-extensions-hmvc/downloads/

step 3. Copy the downloaded core files MY_Loader.php and MY_Router.php to your project under application/core.
        Copy the MX folder from third_party to your project under third_party/
	
step 4. Create a folder name as modules under root(application) folder.
        Under modules folder create your module name along with folders controllers,models and view as follow
        In this example i have create a Users module under modules folder.
	
step 5.MY_Controller.php no need to create if you are not using custome controller. If you want the create MY_Controller.php under application/core directory and past the bellow code 

<?php
class MY_Controller extends MX_Controller {

    function __construct() {
        parent::__construct();
       
    }
}


if you getting error like Call to undefined method MY_Loader::_ci_object_to_array() this 
then replace

return $this->_ci_load(array('_ci_view' => $view, '_ci_vars' => $this->_ci_object_to_array($vars), '_ci_return' => $return)); 

line under third_party/MX/Loader.php line 300 

with

if (method_exists($this, '_ci_object_to_array'))
				{
        return $this->_ci_load(array('_ci_view' => $view, '_ci_vars' => $this->_ci_object_to_array($vars), '_ci_return' => $return));
				} else {
        return $this->_ci_load(array('_ci_view' => $view, '_ci_vars' => $this->_ci_prepare_view_vars($vars), '_ci_return' => $return));
			}
