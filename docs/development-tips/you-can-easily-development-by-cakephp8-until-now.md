# CakePHP2를 PHP 8에서 쉽게 사용하기

CakePHP는 Laravel이 나오기 전 PHP에서 가장 유망한 프레임워크 였고, 많은 프로젝트가 CakePHP로 제작되었고 운용되었습니다. 루비 온 레일즈에서 영감을 받아서 제작된 프레임워크였기 때문에 5분만에 블로그 만들기 튜토리얼이 유명했죠.

하지만, PHP가 표준화 되면서 CakePHP는 CI와 마찬가지로 Laravel 에 그 영광을 돌리게 됩니다. CakePHP와 CI는 Composer나 PSR이 탄생하기 전에 나왔기 때문에 애초에 Laravel의 확장성에는 당할 수가 없였죠. 반면 CRUD 베이스의 프로젝트에서는 아직도 강점을 보이고 있으나, PHP 시장은 두개의 프레임워크가 살아남을 만한 크기가 아닙니다. 완전한 승자 독식이죠.

10년 정도 개발자의 사랑을 받아온 CakePHP는 4.x가 나왔지만 가장 유명한 버전은 2.x며, 공식적인 지원이 끝났으나 오픈소스 커뮤니티에서 PHP 8을 지원하는 버전이 유지되고 있습니다.

하위 호환을 보장하면서 쉽게 PHP 8에서 기존 CakePHP 2.x 코어를 업데이트 하는 방법을 소개합니다.

## CakePHP 2.x 를 업데이트 하고 PHP 8에서 구동하기

CakePHP 2.x를 유지하는 저장소는 [kamilwylegala/cakephp2-php8](https://github.com/kamilwylegala/cakephp2-php8) 입니다.

CakePHP는 Composer를 사용하지 않지만, composer.json을 만든 후 아래와 같은 커맨드를 추가합니다.

```json
{
	"require": {
		"cakephp/cakephp": "dev-master as 2.10.24",
	},
    "scripts": {
		"cake": "cp -r vendors/cakephp/cakephp/lib/Cake lib",
	},
	"repositories": [
        {
            "type": "vcs",
            "url": "https://github.com/kamilwylegala/cakephp2-php8"
        }
    ]
}
```

그 후에는 이래의 커맨드로 쉽게 업데이트 할 수 있습니다.

```sh
# Update cakephp/cakephp
composer update

# Copy cakephp/cakephp to cake core directory
composer run cake
```

`cp` 대신 `rsync`를 사용하거나 혹은 `composer update`의 hook 메쏘드로 카피를 하면 `composer update` 를 할 때마다 자동으로 업데이트가 가능합니다.

## 소감

자바 스프링을 모방한 CakePHP 3.x 나 Composer를 적극 활용한 4.x 을 쓰는 것은 전 추천하지 않습니다. Laravel이 더 나은 대안이기 때문입니다.

반면 기존에 CakePHP 2.x로 만들어진 큰 프로젝트가 있다면 구지 Laravel로 이전하기 보다는 PHP 8에서 운용하는 것이 더 좋은 선택지가 될 수도 있습니다.

Laravel로 이전한다는 것은 생각처럼 쉬운 일이 아니거든요. :)
