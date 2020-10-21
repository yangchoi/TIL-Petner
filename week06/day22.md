#### 루비 코드에 대해 
- 별 다섯개 리뷰를 뽑아 현재 리뷰를 기준으로 이후, 이전 버튼을 누르면 다음 리뷰와 이전 리뷰 보여주기 

```ruby

  def show
    reviews = Review.where(rating: 5).joins(:user, :petner)
    @reviews = reviews
    @review = Review.find_by(id: params[:id]) if params[:id].present?

    current_id = @review.id
    @next_review = next_review(reviews, current_id)
    @previous_review = previous_review(reviews, current_id)

  end

  def next_review(reviews, current_id)
    next_review = reviews.where("reviews.id > ? ", current_id).order(created_at: :asc).first
    next_review_id = nil
    next_review_id = next_review.id if next_review.present?
    return next_review_id
  end

  def previous_review(reviews, current_id)
    @previous_review_id = reviews.where("reviews.id < ? ", current_id).order(created_at: :desc).first.id 
  end
  
```

