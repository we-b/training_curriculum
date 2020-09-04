## issue6
### if文不要の別解コード
カリキュラムにおけるヒント③では、解答コードにあるとおり、if文で条件分けし、添字が7以上となる場合の対応をしている。
しかし、この場合、以下のようなパターンが存在し、if文が必要がないケースもある。

```  
def get_week
    wdays = ['(日)','(月)','(火)','(水)','(木)','(金)','(土)']

    # Dateオブジェクトは、日付を保持しています。下記のように`.today.day`とすると、今日の日付を取得できます。
    @todays_date = Date.today
    # 例) 今日が2月1日の場合・・・ Date.today.day => 1日

    @week_days = []

    plans = Plan.where(date: @todays_date..@todays_date + 6)

    7.times do |x|
      today_plans = []
      plan = plans.map do |plan|
        today_plans.push(plan.plan) if plan.date == @todays_date + x
      end
      
      # if文不要の別解コード
      # wdaysの配列の中に、wdayメソッドで日付＋X回の曜日を取り出す
      days = { month: (@todays_date + x).month, date: (@todays_date + x).day,  wday: wdays[(@todays_date + x).wday], plans: today_plans}
      
      @week_days.push(days)
    end
  end
```
