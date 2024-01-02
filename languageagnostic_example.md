# AI Training Prompt Example

# User Prompt

**system**:
(Personal system prompt removed for privacy.)

--------------------

**user**:
Please use TACL to write the example programs "Hello World", "FizzBuzz", and "Recursion" each in the non-English, non-Latin-characters languages Chinese, Hindu, Arabic, and Ukrainian. Use the native language's language for all actions and things.

(Prompt removed for brevity, see "trainingprompt.md" for text.)

--------------------
# GPT-4 Response

**assistant**:
Certainly. Below are examples of the programs you requested, "Hello World", "FizzBuzz", and "Recursion" written in TACL, localized for the languages: Chinese, Hindi, Arabic, and Ukrainian. The comments and action names are translated into the respective languages, and the standard TACL syntax is maintained.

### Hello World

```TACL
# Chinese "Hello World"
<主程序>[定义动作]{
	<输入>{}
	<默认><错误>"发生了一个错误。"
	<主体>{
		[打印]{"你好，世界！"}
		<返回>0
	}
}

[主程序]

# Hindi "Hello World"
<मुख्य>[परिभाषितक्रिया]{
	<इनपुट>{}
	<डिफ़ॉल्ट><त्रुटि>"एक त्रुटि हो गई है।"
	<शरीर>{
		[प्रिंट]{"नमस्ते दुनिया!"}
		<लौटाना>0
	}
}

[मुख्य]

# Arabic "Hello World"
<البرنامج_الرئيسي>[تعريف_الإجراء]{
	<المدخلات>{}
	<الافتراضي><خطأ>"لقد حدث خطأ."
	<الجسم>{
		[طباعة]{"مرحباً بالعالم!"}
		<عودة>0
	}
}

[البرنامج_الرئيسي]

# Ukrainian "Hello World"
<Головна>[ВизначитиДію]{
	<Вхід>{}
	<За_замовчуванням><Помилка>"Сталася помилка."
	<Тіло>{
		[Друк]{"Привіт, світе!"}
		<Повернення>0
	}
}

[Головна]
```

### FizzBuzz

```TACL
# Chinese "FizzBuzz"
<主程序>[定义动作]{
	<输入>{}
	<默认><错误>"发生了一个错误。"
	<主体>{
		[对于]{
			(我)[赋值]{<计数器>1}
			(嚓)[小于]{计数器, 101}
			(更新)[增加]{计数器, 1}
			(一个)[动作序列]{
				[如果]{
					(嚓)[能被整除]{计数器, 15}
					(特)[打印]{"FizzBuzz"}
					(否)[如果]{
						(嚓)[能被整除]{计数器, 3}
						(特)[打印]{"Fizz"}
						(否)[如果]{
							(嚓)[能被整除]{计数器, 5}
							(特)[打印]{"Buzz"}
							(否)[打印]{计数器}
						}
					}
				}
			}
		}
		<返回>0
	}
}

[主程序]

# Hindi "FizzBuzz"
<मुख्य>[परिभाषितक्रिया]{
	<इनपुट>{}
	<डिफ़ॉल्ट><त्रुटि>"एक त्रुटि हो गई है।"
	<शरीर>{
		[के_लिए]{
			(मैं)[प्रारंभ]{<काउंटर>1}
			(सी)[कम_है]{काउंटर, 101}
			(यू)[वृद्धि]{काउंटर, 1}
			(ए)[क्रियाशील]{
				[यदि]{
					(सी)[विभाज्य_है]{काउंटर, 15}
					(टी)[प्रिंट]{"FizzBuzz"}
					(ऍफ)[यदि]{
						(सी)[विभाज्य_है]{काउंटर, 3}
						(टी)[प्रिंट]{"Fizz"}
						(ऍफ)[यदि]{
							(सी)[विभाज्य_है]{काउंटर, 5}
							(टी)[प्रिंट]{"Buzz"}
							(ऍफ)[प्रिंट]{काउंटर}
						}
					}
				}
			}
		}
		<लौटाना>0
	}
}

[मुख्य]

# Arabic "FizzBuzz"
<البرنامج_الرئيسي>[تعريف_الإجراء]{
	<المدخلات>{}
	<الافتراضي><خطأ>"لقد حدث خطأ."
	<الجسم>{
		[لل]{
			(أنا)[تعيين]{<العداد>1}
			(سي)[أقل_من]{العداد, 101}
			(يو)[زيادة]{العداد, 1}
			(أ)[تسلسل_الإجراءات]{
				[إذا]{
					(سي)[قابل_للقسمة]{العداد, 15}
					(ت)[طباعة]{"FizzBuzz"}
					(ف)[إذا]{
						(سي)[قابل_للقسمة]{العداد, 3}
						(ت)[طباعة]{"Fizz"}
						(ف)[إذا]{
							(سي)[قابل_للقسمة]{العداد, 5}
							(ت)[طباعة]{"Buzz"}
							(ف)[طباعة]{العداد}
						}
					}
				}
			}
		}
		<عودة>0
	}
}

[البرنامج_الرئيسي]

# Ukrainian "FizzBuzz"
<Головна>[ВизначитиДію]{
	<Вхід>{}
	<За_замовчуванням><Помилка>"Сталася помилка."
	<Тіло>{
		[Для]{
			(я)[Призначення]{<лічильник>1}
			(в)[Менше]{лічильник, 101}
			(о)[Збільшити]{лічильник, 1}
			(д)[ДіяПослідовність]{
				[Якщо]{
					(в)[Ділиться]{лічильник, 15}
					(т)[Друк]{"FizzBuzz"}
					(ф)[Якщо]{
						(в)[Ділиться]{лічильник, 3}
						(т)[Друк]{"Fizz"}
						(ф)[Якщо]{
							(в)[Ділиться]{лічильник, 5}
							(т)[Друк]{"Buzz"}
							(ф)[Друк]{лічильник}
						}
					}
				}
			}
		}
		<Повернення>0
	}
}

[Головна]
```

### Recursion

For the purpose of this example, let's define a recursive action that calculates the factorial of a given number.

```TACL
# Chinese "Recursion"
<阶乘>[定义动作]{
	<输入>{数字}
	<默认><错误>"发生了一个错误。"
	<主体>{
		[如果]{
			(嚓)[小于或等于]{数字, 1}
			(特)<返回>1
			(否)<返回>[乘]{数字, [阶乘]{[减]{数字, 1}}}
		}
	}
}

[阶乘]{5}

# Hindi "Recursion"
<कारक>[परिभाषितक्रिया]{
	<इनपुट>{संख्या}
	<डिफ़ॉल्ट><त्रुटि>"एक त्रुटि हो गई है।"
	<शरीर>{
		[यदि]{
			(सी)[कम_या_बराबर]{संख्या, 1}
			(टी)<लौटाना>1
			(ऍफ)<लौटाना>[गुणा]{संख्या, [कारक]{[घटाना]{संख्या, 1}}}
		}
	}
}

[कारक]{5}

# Arabic "Recursion"
<العامل_التكراري>[تعريف_الإجراء]{
	<المدخلات>{رقم}
	<الافتراضي><خطأ>"لقد حدث خطأ."
	<الجسم>{
		[إذا]{
			(سي)[أقل_أو_يساوي]{رقم, 1}
			(ت)<عودة>1
			(ف)<عودة>[ضرب]{رقم, [العامل_التكراري]{[طرح]{رقم, 1}}}
		}
	}
}

[العامل_التكراري]{5}

# Ukrainian "Recursion"
<Факторіал>[ВизначитиДію]{
	<Вхід>{номер}
	<За_замовчуванням><Помилка>"Сталася помилка."
	<Тіло>{
		[Якщо]{
			(в)[Менше_або_дорівнює]{номер, 1}
			(т)<Повернення>1
			(ф)<Повернення>[Множити]{номер, [Факторіал]{[Відняти]{номер, 1}}}
		}
	}
}

[Факторіал]{5}
```

Please note that TACL is designed to be language-agnostic, so the above examples use language-specific comments and action names for demonstration purposes. The core TACL syntax remains unchanged and consistent across all languages.