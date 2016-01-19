* API reference

```cpp
namespace msm {
    template <class T> // requires T to have T.configure()
    class sm {
    public:
      using events; // list of supported events

      template<class... TDeps> // no requirements
      explicit sm(TDeps&&...) noexcept; // action/guards dependencies
      sm_impl(const sm &) = delete;
      sm_impl(sm &&) = default;

      template <class TEvent> // no requirements, returns whether event was handled or not
      bool process_event(const TEvent &) noexcept;

      template <class TVisitor> // requires TVisitor to be callable with auto
      void visit_current_states(const TVisitor &) const noexcept;

      template <class TFlag> // no requirements, returns whether active state has TFlag or not
      bool is(const TFlag &) const noexcept;
    };

    template <class... Ts> // requires Ts to have Ts::src_state
                           //                   , Ts::dst_state
                           //                   , Ts::event
                           //                   , Ts::deps
                           //                   , Ts.execute(...)
    auto make_transition_table(Ts...) noexcept;

    action process_event;

    template <class TEvent> // no requirements
    auto event{};

    template <class T> // no requirements
    using state;

    template <class T, T...>
    state<T...> operator""_s(); // create a state, ex. "idle"_s

    state initial;

    template <class T> // requires T to be callable and returns bool
    auto operator!(const T &) noexcept;

    template <class T1, class T2> // requires T1, T2 to be callable and returns bool
    auto operator&&(const T1 &, const T2 &) noexcept;

    template <class T1, class T2> // requires T1, T2 to be callable and returns bool
    auto operator||(const T1 &, const T2 &) noexcept;

    template <class T1, class T2> // requires T1, T2 to be callable
    auto operator, (const T1 &t1, const T2 &t2) noexcept;
}
```