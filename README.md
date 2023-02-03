# Models_Projrect
 D2.9 project SK

Команды, которыми я пользовался для записи данных в БД

from news.models import *

u1 = User.objects.create_user(username='Роман')
u2 = User.objects.create_user(username='Дмитрий')
_________________________________________________

Author.objects.create(authorUser=u1)
Author.objects.create(authorUser=u2)
____________________________________

Category.objects.create(name='Игры')
Category.objects.create(name='IT')
Category.objects.create(name='Техника')
Category.objects.create(name='Машины')
______________________________________

author = Author.objects.get(id=1)
author2 = Author.objects.get(id=2)
____________________________________

Post.objects.create(author=author, categoryType='NW', title='Релиз DEAD SPACE REMAKE!', text='Вышла очень классная и красивая DEAD SPACE REMAKE')
Post.objects.create(author=author, categoryType='AR', title='Чем хорош DEAD SPACE REMAKE?', text='Бла-бла-бла 10/10')
Post.objects.create(author=author2, categoryType='AR', title='Опыть использования BMW M5', text='Бла-бла-бла СЛОМАЛАСЬ')
___________________________________________________________________

Post.objects.get(id=1).postCategory.add(Category.objects.get(id=1))
Post.objects.get(id=1).postCategory.add(Category.objects.get(id=2))

Post.objects.get(id=2).postCategory.add(Category.objects.get(id=3))
Post.objects.get(id=2).postCategory.add(Category.objects.get(id=4))

Post.objects.get(id=3).postCategory.add(Category.objects.get(id=1))
Post.objects.get(id=3).postCategory.add(Category.objects.get(id=2))
___________________________________________________________________

Comment.objects.create(commentPost=Post.objects.get(id=1), commentUser=Author.objects.get(id=1).authorUser, text='бла-бла')
Comment.objects.create(commentPost=Post.objects.get(id=1), commentUser=Author.objects.get(id=2).authorUser, text='бла-бла')
Comment.objects.create(commentPost=Post.objects.get(id=2), commentUser=Author.objects.get(id=1).authorUser, text='бла-бла')
Comment.objects.create(commentPost=Post.objects.get(id=2), commentUser=Author.objects.get(id=2).authorUser, text='бла-бла')
Comment.objects.create(commentPost=Post.objects.get(id=3), commentUser=Author.objects.get(id=1).authorUser, text='бла-бла')
Comment.objects.create(commentPost=Post.objects.get(id=3), commentUser=Author.objects.get(id=2).authorUser, text='бла-бла')
___________________________________________________________________

Comment.objects.get(id=1).like()
Comment.objects.get(id=1).like()
Comment.objects.get(id=1).like()
Comment.objects.get(id=1).dislike()

Comment.objects.get(id=2).like()
Comment.objects.get(id=2).dislike()
Comment.objects.get(id=2).like()
Comment.objects.get(id=2).dislike()
Comment.objects.get(id=2).dislike()

Comment.objects.get(id=3).like()
Comment.objects.get(id=3).like()
Comment.objects.get(id=3).like()
Comment.objects.get(id=3).like()

Comment.objects.get(id=4).like()    
Comment.objects.get(id=4).like()
Comment.objects.get(id=4).like()
Comment.objects.get(id=4).like()
Comment.objects.get(id=4).like()

Comment.objects.get(id=5).like()
Comment.objects.get(id=5).like()
Comment.objects.get(id=5).like()
Comment.objects.get(id=5).dislike() 
Comment.objects.get(id=5).like()
Comment.objects.get(id=5).dislike()

Comment.objects.get(id=6).like()
Comment.objects.get(id=6).like()
Comment.objects.get(id=6).dislike()
___________________________________

Comment.objects.get(id=1).rating
Comment.objects.get(id=2).rating
Comment.objects.get(id=3).rating
Comment.objects.get(id=4).rating
Comment.objects.get(id=5).rating
Comment.objects.get(id=6).rating
___________________________________

a = Author.objects.get(id=1)
b = Author.objects.get(id=2)

a.update_rating()
b.update_rating()

a.ratingAuthor
b.ratingAuthor
___________________________________

Post.objects.get(id=1).like()
Post.objects.get(id=1).like()
Post.objects.get(id=1).like()

Post.objects.get(id=2).like()
Post.objects.get(id=2).dislike()
Post.objects.get(id=2).like()

Post.objects.get(id=3).like()
Post.objects.get(id=3).like()

a.update_rating()
b.update_rating()

a.ratingAuthor
b.ratingAuthor
______________________________________

a = Author.objects.order_by('-ratingAuthor')[:1]
for i in a:
	i.ratingAuthor
	i.authorUser.username

потом мне подсказали вот такой вариант: Author.objects.order_by('-rating').values('authorUser__username', 'rating')[0]
____________________________________________________

Post.objects.order_by('-rating').values('dateCreation', 'author__authorUser__username', 'rating', 'title')[0]

Post.objects.order_by('-rating')[0].preview()
__________________________________________________

Comment.objects.order_by('-rating').values('dateCreation', 'commentUser__username', 'rating', 'text')