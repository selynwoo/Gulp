#Javascript 명령어 
- `gulp-concat` (병합)
- `gulp-uglify` (압)
<br>

## gulp-concat (병합) 
- **설치 [ cmd : `npm i -D gulp-concat` ]**

- **Modules 호출**
```md
var gulp = require('gulp'),
    concat = require('gulp-concat');
```

- **지정한 js 병합** <br>
```md
gulp.task('combine:js', function(){
	gulp
		.src(['./src/domheler-id.js', './src/domheler-tag.js'])
		.pipe(concat('combined.js'))
		.pipe(gulp.dest('./dist'));
});
```

- **모든 js 병합** <br>
```md
gulp.task('combine:js', function(){
	gulp
		.src('./src/*.js') 
		.pipe(concat('combined.js'))
		.pipe(gulp.dest('./dist'));
});
```

- **특정파일 우선적 병합** <br>
```md
gulp.task('combine:js', function(){
	gulp
		.src(['./src/domhelper-prevEl.js', './src/*.js']) 
		.pipe(concat('combined.js'))
		.pipe(gulp.dest('./dist'));
});
```

- **하위디렉터리 모든 js 병합** <br>
```md
gulp.task('combine:js', function(){
	gulp
		.src('src/js/libs/**/*.js') //src 디렉터리의 js/libs 하위 디렉터리를 생성 후 실행 후 확인
		.pipe(concat('combined.js'))
		.pipe(gulp.dest('./dist'));
});
```
<br>
## gulp-uglify (압축) 
- **설치 [ cmd : `npm i -D gulp-uglify` ]**

- **Modules 호출**
```md
var gulp = require('gulp'),
    uglify = require('gulp-uglify'),
    concat = require('gulp-concat');
```

- **압축** <br>
```md
gulp.task('combine:js', function(){
	gulp
		.src('src/js/libs/**/*.js')
		.pipe(concat('combined.js'))
		.pipe(uglify())
		.pipe(gulp.dest('./dist'));
});
```

- **압축 조건** <br>
```md
gulp.task('combine:js', function(){
	gulp
		.src('src/js/libs/**/*.js')
		.pipe(concat('combined.js'))
		.pipe(uglify({
			mangle : false, //변수, 매개변수 축약여부
			preserveComments: 'all' // 'all' : 모든주석 보존, 'some' : !(느낌표)가 붙은 주석만 보존
		}))
		.pipe(gulp.dest('./dist'));
});
```


