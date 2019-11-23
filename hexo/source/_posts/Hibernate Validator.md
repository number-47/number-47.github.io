---
title: Hibernate Validator
tags: Hibernate Validator
categories: Hibernate Validator
copyright: true
comment: true
---

# Hibernate Validator

| 注解                                        | 作用                                                         |
| ------------------------------------------- | ------------------------------------------------------------ |
| @Null                                       | 值必须为空                                                   |
| @Pattern(regex=)                            | 字符串必须匹配正则表达式                                     |
| @Size(min=,max=)                            | 集合的元素数量必须在min和max之间                             |
| @CreditCardNumber(ignoreNonDigitCharacters) | 字符串必须是信用卡号（按美国的标准验证的）                   |
| @Email                                      | 字符串必须是Email地址                                        |
| @Length(min=,max=)                          | 检查字符串的长度                                             |
| @NotBlank                                   | 字符串必须有字符                                             |
| @NotEmpty                                   | 字符串不为null,集合有元素                                    |
| @Range(min=,max=)                           | 数字必须大于等于min,小于等于max                              |
| @SafeHtml                                   | 字符串是安全的html                                           |
| @URL                                        | 字符串是合法的URL                                            |
| @NotNull                                    | 值不能为空                                                   |
| @AssertFalse                                | 值必须为false                                                |
| @AssertTrue                                 | 值必须为true                                                 |
| @DecimalMax(value=,inclusive=)              | 值必须小于等于（inclusive=true）/小于（inclusive=false）value属指定的值，可以注解在字符串类型的属性上 |
| @DecimalMin(value=,inclusive=)              | 值必须大于等于（inclusive=true）/大于（inclusive=false）value属指定的值，可以注解在字符串类型的属性上 |
| @Digits(integer=,fraction=)                 | 数字格式检查。integer指定整数部分的最大长度，fraction指定小数部分的最大长度 |
| @Future                                     | 值必须是未来的日期                                           |
| @Past                                       | 值必须是过去的日期                                           |
| @Max(value=)                                | 值必须小于等于value指定的值。不能注解在字符串类型的属性上。  |
| @Min(value=)                                | 值必须大于等于value指定的值。不能注解在字符串类型的属性上。  |
|                                             |                                                              |

## 通过@Valid,BindingResult使用校验/@JsonView指定属性的显示

Public class User{

```
    public interface UserSimpleView{};

    public interface UserDetailView extends UserSimpleView{};
```

```java
    /**
     * @NotBlank校验不为空
     */
	@NotBlank
	private String password;
	private String userName;

	@JsonView(UserSimpleView.class)
	public String getUserName() {
		return userName;
	}

	public void setUserName(String userName) {
		this.userName = userName;
	}

	@JsonView(UserDetailView.class)
	public String getPassword() {
		return password;
	}

	public void setPassword(String password) {
		this.password = password;
	}
```

}



```java
@RestController
@RequestMapping("/user")
public class UserController {


	@PostMapping
	@JsonView(User.UserSimpleView.class) //显示名称
	public User userCreate(@Valid @RequestBody User user, BindingResult errors){
		//捕获没有通过校验的错误
		if (errors.hasErrors()){
			errors.getAllErrors().stream().forEach(error -> System.out.println(error.getDefaultMessage()));
		}
		System.out.println(user.getId());
		System.out.println(user.getUserName());
		System.out.println(user.getPassword());
		System.out.println(user.getBirthDay());
		user.setId("1");
		return user;
	}
    
   /**
	 *
	 * @param userId 通过正则表达式 只能接受数字
	 * @return
	 */
	@GetMapping("/{id:\\d+}")
	@JsonView(User.UserDetailView.class) //显示名称和密码
	public User getInfo(@PathVariable(name = "id") String userId){
		User user = new User();
		user.setUserName("JOJO");
		return user;
	}
}
```