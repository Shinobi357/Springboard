# **Production Deployment Architecture for Car Price Prediction Model**

## **Overview**

The objective of this project is to take the machine learning prototype developed in Phase 1 and design a production-ready architecture capable of serving real-time vehicle price predictions.

The current prototype predicts vehicle prices based on vehicle characteristics such as brand, model, year, engine size, fuel type, transmission type, mileage, and condition. The production system must be scalable, reliable, maintainable, and capable of supporting future model retraining and monitoring.

---

# **Architecture Diagram**

               User / Client  
                       |  
                       v  
                 Web Application  
                       |  
                       v  
                AWS API Gateway  
                       |  
                       v  
                AWS Lambda Layer  
                       |  
                       v  
             SageMaker Endpoint  
                       |  
                       v  
          Car Price Prediction Model  
                       |  
                       v  
              Predicted Vehicle Price

       \-------------------------------  
       Monitoring and Data Pipeline  
       \-------------------------------

Vehicle Data \+ Prediction Logs  
               |  
               v  
           Amazon S3  
               |  
               v  
      CloudWatch Monitoring  
               |  
               v  
       Model Performance Review  
               |  
               v  
        Model Retraining  
               |  
               v  
        New Model Artifact  
               |  
               v  
     SageMaker Redeployment

---

# **Major Components**

The production system consists of the following components:

1. Web Application  
2. AWS API Gateway  
3. AWS Lambda  
4. AWS SageMaker Endpoint  
5. Trained Machine Learning Model  
6. Amazon S3 Storage  
7. Amazon CloudWatch Monitoring  
8. Model Retraining Pipeline

### **Inputs**

The system receives:

* Brand  
* Model  
* Year  
* Engine Size  
* Fuel Type  
* Transmission  
* Mileage  
* Condition

### **Output**

The system returns:

* Predicted vehicle price

---

# **Data Storage**

Amazon S3 will serve as the primary storage location.

The following data will be stored:

* Raw vehicle datasets  
* Cleaned datasets  
* Training datasets  
* Prediction logs  
* Model artifacts  
* Retraining datasets

S3 was selected because it is scalable, durable, and integrates directly with SageMaker.

---

# **Data Flow**

The user submits vehicle information through a web application.

The request flows through:

Web Application → API Gateway → Lambda → SageMaker Endpoint

The trained model generates a prediction and returns the estimated vehicle price.

Prediction requests and logs are stored in S3 and monitored through CloudWatch.

---

# **Machine Learning Lifecycle**

The model lifecycle includes:

1. Data Collection  
2. Data Validation  
3. Data Preprocessing  
4. Model Training  
5. Hyperparameter Tuning  
6. Model Evaluation  
7. Deployment  
8. Monitoring  
9. Retraining  
10. Redeployment

Deployment is not the end of the process. Once deployed, the model must be continuously monitored and improved.

---

# **Retraining Strategy**

The model should be retrained when:

* Prediction accuracy drops below acceptable thresholds  
* Significant data drift is detected  
* New vehicle pricing data becomes available  
* Quarterly retraining review occurs

Recommended schedule:

* Monthly monitoring review  
* Quarterly retraining evaluation

Retraining data will be collected from:

* New vehicle listings  
* Updated vehicle prices  
* New mileage information  
* Market pricing updates

The retraining datasets will be stored and versioned in Amazon S3.

---

# **Model Evaluation and Redeployment**

Before a retrained model is deployed, it must be evaluated against the current production model.

Evaluation metrics include:

* R² Score  
* Mean Absolute Error (MAE)  
* Root Mean Squared Error (RMSE)

The retrained model will only replace the production model if it demonstrates improved performance and generalization.

Approved models will be stored as versioned artifacts in Amazon S3 and deployed through SageMaker.

---

# **Monitoring and Debugging**

The production system will be monitored using:

* Amazon CloudWatch  
* SageMaker Monitoring

Metrics include:

* API response times  
* Endpoint latency  
* Error rates  
* Request volume  
* Data drift  
* Prediction distributions

CloudWatch logs will be used for troubleshooting and debugging production issues.

---

# **Technologies Used**

* Python  
* Scikit-learn  
* Jupyter Notebook  
* AWS SageMaker  
* Amazon S3  
* AWS Lambda  
* AWS API Gateway  
* Amazon CloudWatch  
* GitHub

AWS SageMaker was selected because it was used throughout the bootcamp and provides built-in support for model deployment, monitoring, retraining, and MLOps workflows.

---

# **Cost Estimate**

### **Development Time**

* Architecture Design: 4–8 hours  
* Initial Deployment: 8–12 hours  
* Monitoring Setup: 2–4 hours

### **Cloud Costs**

For a small prototype:

* Amazon S3: Low cost  
* API Gateway: Low cost  
* Lambda: Low cost  
* SageMaker Endpoint: Primary operational cost  
* CloudWatch Monitoring: Low cost

The estimated monthly cost for a low-volume prototype environment would be relatively low, with SageMaker endpoint usage representing the largest expense.

---

# **Scalability, Fault Tolerance, and Future Enhancements**

The architecture is designed to scale by increasing SageMaker endpoint capacity as request volume grows.

Potential future enhancements include:

* Batch prediction processing  
* Mobile application integration  
* Real-time vehicle market feeds  
* Automated retraining pipelines  
* Multiple model versions for A/B testing

If usage increases significantly, the architecture could be expanded using containerized services and Kubernetes-based deployments to improve fault tolerance and resilience.

---

# **Design Justification**

AWS SageMaker was selected because it provides a complete machine learning deployment environment and aligns with the technologies used throughout the bootcamp. The architecture supports model deployment, monitoring, retraining, artifact management, and scalability while minimizing infrastructure complexity.

This design provides a realistic path for moving the Phase 1 prototype into a production environment while supporting long-term model maintenance and continuous improvement.

