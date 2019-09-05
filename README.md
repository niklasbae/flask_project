# Python Flask Project

After using blueprints:

To do database changes in the Terminal:

from app import create_app, db

app = create_app()

ctx = app.app_context()

ctx.push()

db.create_all()

ctx.pop()

exit()

Deployment:

https://youtube.com/watch?v=goToXTC96Co&list=PL-osiE80TeTs4UjLw5MM6OjgkjFeUxCYH&index=13
