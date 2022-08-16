# Esquema de vistas.

---



## AuthenticatedAPITestCase.

```python
class AuthenticatedApiTestCase(APITestCase):

    """
    This class help us to authenticate the requests of the endpoint, to can test the views.
    The objective is to inherit from this class, which will be in charge of authenticating the calls.
    """

    endpoint_name = None

    def setUp(self) -> None:
        self.password = '123456'
        self.user = UserFactory(password=self.password)

        if self.endpoint_name is not None:
            self.url = reverse(self.endpoint_name)

        login_body = {
            'username': self.user.username,
            'password': self.password
        }
        login_url = reverse('token_obtain_pair')
        self.user_token = self.client.post(login_url, login_body, format='json').data.get('access', None)
        self.client.credentials(HTTP_AUTHORIZATION=f'Bearer {self.user_token}')

    def forbidden_client(self):
        self.client.credentials(HTTP_AUTHORIZATION='')

```



## Create view.

```python
```



## Delete view.



## Update view.



## List view.



## Info view.





- Agrupar los tests según el campo a testear.

  - ```python
    # Field_1
    # TEST THE MANDATORY CHARACTER OF THE FIELD.
    def test_create_field_view_return_400_for_N1field_not_provided(self):
        before_count = Course.objects.count()
        self.body['fielf_name'] = None
        response = self.client.post(self.url, self.body, format='json')
        self.assertEqual(Course.objects.count(), before_count)
        self.assertEqual(status.HTTP_400_BAD_REQUEST, response.status_code)
        
    # TEST THE VALIDATION OF THE CORRECT OBJECT-TYPE. 
    def test_create_object_view_return_400_for_N1field_wrong_type(self):
        before_count = Course.objects.count()
        self.body['education_center'] = [0, 1, 2] # OR ANOTHER WRONG TYPE.
        response = self.client.post(self.url, self.body, format='json')
        self.assertEqual(Course.objects.count(), before_count)
        self.assertEqual(status.HTTP_400_BAD_REQUEST, response.status_code)
    
    # TEAT THE UNIQUE CHARACTER OF THE FIELD.
    def test_create_object_view_return_400_for_N1field_is_not_unique(self):
            new_object = ObjectFactory()
            before_count = Object.objects.count()
    
            self.body['N1field'] = new_object.N1field
            response = self.client.post(self.url, self.body, format='json')
            self.assertEqual(Object.objects.count(), before_count)
            self.assertEqual(status.HTTP_400_BAD_REQUEST, response.status_code)
        
    # Field_2
    # TEST THE OPTIONAL CHARACTER OF THE FIELD.
    def test_create_object_view_return_201_for_N1field(self):
        before_count = Course.objects.count()
        self.body['ects_credits'] = None
        response = self.client.post(self.url, self.body, format='json')
        self.assertEqual(Course.objects.count(), before_count + 1)
        self.assertEqual(status.HTTP_201_CREATED, response.status_code)
        
    # TEST THE VALIDATION OF THE CORRECT OBJECT-TYPE. 
    ...
    ```

  - 
