# upyun_laravel
upyun for laravel5 2015-02-03

一、修改composer.json文件
  在autoload-dev的classmap中添加app/Libs/Upyun.php，如下：
  
	"autoload-dev": {
		"classmap": [
			"database"
		],
		"classmap": [
			"tests/TestCase.php",
			"app/Libs/Upyun.php"
		]
	},
二、在app目录下添加Libs文件夹，下载Upyun.php文件放到该文件夹下

三、执行php composer.phar install

四、参考ImgController.php写上传文件接口

五、在.env文件增加又拍云文件配置

	UPYUN_BUCKETNAME=又拍云空间名，在又拍云后台管理中添加

	UPYUN_USERNAME=空间的授权用户名

	UPYUN_PASSWORD=授权用户密码
	
六、上传示例
	
	use App\Http\Requests\StoreInfoRequest;//验证提交数据完整性文件
	use App\Http\Controllers\Upload\ImgController;//使用统一上传接口
	/*
	*保存数据，需要验证提交数据是否正确，有图片上传则调用统一上传接口上传文件
	*/
	public function store(StoreInfoRequest $InfoRequest,ImgController $imgController){
		$file = $imgController->uploadImg('thumbnail','',$InfoRequest);
		if($file){
			$data['thumbnail'] = $file;
		}
		/*
		
		业务逻辑代码
		
		*/
	}
