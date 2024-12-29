Nguyễn Văn Tùng

Deha-Academy-php-RestfullApi-Lab1

## Getting Started
    `git clone https://github.com/Tung-Pro/Deha-Academy-php-RestfullApi-Lab1.git` 

    php artisan serv

## Tools/commands used

### Create Migration:

    php artisan make:migration create_posts_table
    php artisan make:migrate

### Tạo Model và Controller:

    php artisan make:model Post
    php artisan make:controller API/PostController --api

### Install Api

    php artisan install:api

### Create Factory and Seed dữ liệu mẫu

    php artisan make:factory PostFactory
    php artisan tinker
    App\Models\Post::factory(100)->create()

### Create Resource and Collection

    php artisan make:resource PostResource
    php artisan make:resource PostCollection

### Create Form Request Validation

    php artisan make:request StorePostRequest
    php artisan make:request UpdatePostRequest
    

## Using Postman to test API

Get list Post

![image](https://github.com/user-attachments/assets/2ffd4bc2-5bfc-41ab-82e2-3f2dd939f95c)

Add Post

![image](https://github.com/user-attachments/assets/c8624543-b509-43f0-9369-b93cca9f69e8)

Update Post by PUT

![image](https://github.com/user-attachments/assets/6d5dff00-dd74-4907-b630-b42dafcc078a)

Update Post by PATCH

![image](https://github.com/user-attachments/assets/1b26c389-a36f-463f-9fa0-eb471d0aa1f2)

Get Post

![image](https://github.com/user-attachments/assets/7b24bd68-280d-48dd-846f-30397dcd69ca)

Delete Post

![image](https://github.com/user-attachments/assets/eefce8b5-a27e-4651-a03c-57ba906ca071)

## Feature Test

### Create test

    php artisan make:test Posts/CreatePostTest
    php artisan make:test Posts/DeletePostTest
    php artisan make:test Posts/GetListPostTest
    php artisan make:test Posts/GetPostTest
    php artisan make:test Posts/UpdatePostTest

### Run test

CreatePostTest

    php artisan test --filter user_can_create_post_if_data_is_valid
    php artisan test --filter user_can_not_create_post_if_name_is_null
    php artisan test --filter user_can_not_create_post_if_body_is_null
    php artisan test --filter user_can_not_create_post_if_data_is_invalid

DeletePostTest

    php artisan test --filter user_can_delete_post_if_post_exits
    php artisan test --filter user_can_not_delete_post_if_post_not_exits

GetListPostTest

    php artisan test --filter user_can_get_list_posts
    
GetPostTest

    php artisan test --filter user_can_not_get_post_if_post_not_exits
    php artisan test --filter user_can_get_post_if_post_exits
    
UpdatePostTest

    php artisan test --filter user_can_update_post_if_post_exits_and_data_is_valid
    php artisan test --filter user_can_not_update_post_if_post_exits_and_name_is_null
    php artisan test --filter user_can_not_update_post_if_post_exits_and_body_is_null
    php artisan test --filter user_can_not_update_post_if_post_exits_and_data_is_not_valid
    php artisan test --filter user_can_not_update_post_if_post_not_exits_and_data_is_valid

## Use handle error (bootstrap/app.php)
    ->withExceptions(function (Exceptions $exceptions) {
            $exceptions->render(function (ModelNotFoundException $e, Request $request) {
                if ($request->is('api/*')) {
                    return response()->json([
                        'status' => 404,
                        'message' => $e->getMessage()
                    ], 404);
                }
            });
            $exceptions->render(function (NotFoundHttpException $e, Request $request) {
                if ($request->is('api/*')) {
                    return response()->json([
                        'status' => 404,
                        'message' => 'Page not found!'
                    ], 404);
                }
            });
        })->create();
