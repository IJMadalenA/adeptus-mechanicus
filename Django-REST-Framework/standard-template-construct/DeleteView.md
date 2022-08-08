# DeleteView.

```python
import logging

# Rest-Framework imported.
from rest_framework import status
from rest_framework.views import APIView
from rest_framework.response import Response
from rest_framework.permissions import IsAuthenticated
from rest_framework.exceptions import (
    ValidationError,
    PermissionDenied
)

# Models imported.
from app.models import <ObjectModel>

# Serializers imported.
from app.serializer.input import <ObjectSerializerInput>

logger = logging.getLogger(__name__)


class ObjectDeleteView(APIView):
    """
    View to delete one object in the database.
    
    Requirements:
    * Requires token authentication.
    * Only users with a specifict permission are able to access to this view.
    """
    
    permission_classes = [IsAuthenticated, ]
    serializer_class = <ObjectSerializerInput>
    
    def delete(self, request):
        """
        Delete the <object> that coincide with the 'id' provide.
        """
        
        try:
            # Validate if the 'id' is provided and if it's in the correct format.
            object_id = request.data.get("id", None)
            
            if not isinstance(object_id, int):
                raise ValidationError(
                	f"Parameter 'object_id' is required and it must be a 'int'. Receive: {type(object_id).__name__}"
                )
                
            # Find the object by it's 'id' and process to delete it.
            delete_object = <ModelObject>.objects.get(id=object_id).delete()
            
            response = Response(
                delete_object
            	status=status.HTTP_204_NO_CONTENT,
            )
            
        # EXCEPTIONS: 
        except ModelObject.DoesNotExist:
            response = Response(
                {
                    "error_code": "ELEMENT_NOT_FOUND",
                    "detail": f"Object with the 'id' provided was not exist."
                },
                status=status.HTTP_404_NOT_FOUND,
            )
        except ValidationError as e:
            response = Response(
                {
                    "error_code": "BAD_REQUEST",
                    "detail": str(e),
                },
                status=status.HTTP_400_BAD_REQUEST,
            )
        except PermissionDenied as e:
            response = Response(
                {
                    "error_code": "USER_UNAUTHORIZED",
                    "detail": str(e),
                },
                status=status.HTTP_401_UNAUTHORIZED,
            )
            
        return response

```

