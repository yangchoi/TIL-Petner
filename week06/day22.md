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

다음 리뷰의 아이디인 next_review_id를 nil로 설정한 다음 <br>
id 값이 nil이 아니고 존재한다면 next_review_id 를 리턴해주고 <br>
만약에 없다면 그대로 nil을 보낸다. 
