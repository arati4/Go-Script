import (
"context"
"fmt"
"log"

"github.com/aws/aws-sdk-go-v2/aws"
"github.com/aws/aws-sdk-go-v2/config"
"github.com/aws/aws-sdk-go-v2/service/s3"
)

func main() {
ctx := context.TODO()

cfg, err := config.LoadDefaultConfig(ctx)
if err != nil {
log.Fatalf("unable to load AWS config: %v", err)
}


s3Client := s3.NewFromConfig(cfg)


output, err := s3Client.ListBuckets(ctx, &s3.ListBucketsInput{})
if err != nil {
log.Fatalf("failed to list buckets: %v", err)
}

fmt.Println("S3 Buckets:")
for _, bucket := range output.Buckets {
fmt.Printf(" - %s (Created on: %s)\n", aws.ToString(bucket.Name), bucket.CreationDate)
}
}
